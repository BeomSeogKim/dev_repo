> 다른 테이블에 존재하는 데이터들을 조합하여 result set을 제공하는 방식

JOIN은 projections를 생성 [[Projections]]


SQL에서는 JOIN 타입을 다음과 같이 정의한다.
- CROSS JOIN
- INNER JOIN
- OUTER JOIN
- NATURAL JOIN
- LATERAL JOIN

### CROSS JOIN
```sql
SELECT
	ranks.name as rank,
	suits.symbol as suit
FROM
	ranks
CROSS JOIN
	suits
ORDER BY
	ranks.rank_value DESC,
	suits.name ASC
```

*theta style* 
```sql
SELECT
	ranks.name as rank,
	suits.symbol as suit
FROM
	ranks, suits
ORDER BY
	ranks.rank_value DESC,
	suits.name ASC
```

Cartesian 곱을 생성하는 Join 방식.

### INNER JOIN
> 외래키와 함께 사용 된다.
> ON 절 조건이 만족하는 값들만 들고 온다.

```sql
SELECT 
	p.id AS post_id
	p.title AS post_title,
	pc.review AS review
FROM
	post p
INNER JOIN 
	post_commnt pc ON pc.post_id = p.id
ORDER BY
	pc.id
```

*theta style*

```sql
SELECT 
	p.id AS post_id
	p.title AS post_title,
	pc.review AS review
FROM
	post p, post_commend pc 
WHERE 
	pc.post_id = p.id
ORDER BY
	pc.id
```

USING
-> 만약 다른 두 테이블에서 JOIN Colum이름이 같다면 USING 키워드를 사용해서 조인 할 수 있음

```sql
SELECT 
	p.id AS post_id
	p.title AS post_title,
	pc.review AS review
FROM
	post p
INNER JOIN USING(post_id)
ORDER BY
	pc.id
```

USING과 ON절을 사용할 때의 차이점 
select * ... 을 했을 때, USING의 경우 동일한 컬럼에 대해 단일 컬럼으로 보여준다. 하지만 ON절을 사용하는 경우 같은 이름의 컬럼이 두개 생긴다. 


### NATURAL JOIN
> 암묵적으로 양쪽 테이블 컬럼 중 같은 이름을 가진 컬럼 값을 ON절 조건으로 사용함.
> 다만 처음에 없던 컬럼이 나중에 추가되었을 때 동일한 컬럼이 있다면 문제가 발생할 수 있다.
> (ex version을 추가하는 경우 등..)
> 다만 사용성이 떨어지기 때문에 사용을 지양하는 편

```sql
SELECT
	p.id AS post_id
	p.title AS post_title,
	l.language AS post_language
FROM post p
NATURAL JOIN localization l 
ORDER BY p.id
```

```sql
SELECT
	p.id AS post_id
	p.title AS post_title,
	l.language AS post_language
FROM post p
JOIN localization l on p.locale = l.locale 
ORDER BY p.id
```

따라서 파생 table을 NATURAL JOIN을 하는 방식으로 사용할 수 있다.

```sql
SELECT *
FROM (
	SELECT
		schemaname,
		tablename,
		indexname,
		indexdef
	FROM pg_indexes
) i 
NATURAL JOIN (
	SELECT 
		schemaname,
		tablename,
		tableowner
	FROM pg_tables
) t 
where tablename = 'post'
```

### LEFT JOIN
> 왼쪽 테이블 중 필터링 기준에 의해 생성된 행을 기준으로 resultset을 생성
> 오른쪽 테이블에 일치하는 행의 열을 기준으로 결과 집합을 생성하거나 불일치하는 경우 NULL

```sql
SELECT 
	p.id AS post_id,
	p.title AS post_title,
	pc.review AS review
FROM post p
LEFT JOIN post_comment pc ON pc.post_id = p.id
ORDER BY p.id, pc.id
```

*equivalent*
```sql
SELECT post_id, post_title, review
FROM (
	SELECT 
		p.id AS post_id, p.title AS post_title,
		pc.review AS review, pc.id AS pc_id
	FROM post p 
	INNER JOIN post_comment pc ON pc.post_id = p.id
	UNION ALL
	SELECT 
		id AS post_id, title as post_title,
		NULL AS review, NULL AS pc_id
	FROM post p 
	WHERE id NOT IN (SELECT post_id FROM post_comment)
)
ORDER BY p.id, pc.id
```

### RIGHT JOIN
> 오른쪽 테이블 중 필터링 기준에 의해 생성된 행을 기준으로 resultset을 생성
> 왼쪽 테이블에 일치하는 행의 열을 기준으로 결과 집합을 생성하거나 불일치하는 경우 NULL

```sql
SELECT 
	p.id AS post_id,
	p.title AS post_title,
	pc.review AS review
FROM post_comment pc
RIGHT JOIN post p ON pc.post_id = p.id
ORDER BY p.id, pc.id
```

### FULL JOIN
> 주어진 JOIN절 조건과 일치하는 지 여부에 관계없이 왼쪽 오른쪽 모두 
> 현재 SQL 쿼리 필터링 기준에 의해 생성된 행을 기반으로 result set 반환
> 단 MySQL 8에서는 사용 불가.

```sql
SELECT 
	p.id AS post_id,
	p.title AS post_title,
	pc.review AS review
FROM post p
FULL JOIN post_comment pc ON pc.post_id = p.id
ORDER BY p.id, pc.id
```

*equivalent*
```sql
SELECT post_id, post_title, review
FROM (
	SELECT 
		p.id AS post_id, p.title AS post_title,
		pc.review AS review, pc.id AS pc_id
	FROM post p 
	LEFT JOIN post_comment pc ON pc.post_id = p.id
	UNION ALL
	SELECT 
		p.id AS post_id, p.title as post_title,
		pc.review AS review, pc.id AS pc_id
	FROM post p 
	RIGHT JOIN post_comment pc ON pc.post_id = p.id
)
ORDER BY p.id, pc.id
```

### LATERAL JOIN 
> subquery가 외부 쿼리 (from 절)의 행을 교차 참조 할 수 있도록 허용하면서
> 하위 쿼리와 외부 쿼리 결과 집합을 조인함

```sql
SELECT 
	b.id as blog_id,
	age_in_years,
	date(created_on + (age_in_years + 1) * interval '1 year') AS next_anniversary,
	date(created_on + (age_in_years + 1) * interval '1 year') - 
	date(now()) AS days_to_next_anniversary
FROM blog b
CROSS JOIN LATERAL (
	SELECT
		cast(extract(YEAR FROM age(now(), b.created_on)) AS int) AS age_in_years
) AS t
ORDER BY blog_id
```