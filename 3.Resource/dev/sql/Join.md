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

# INNER JOIN
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