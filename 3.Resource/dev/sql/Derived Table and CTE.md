Derived Table 
- subquery에 의해 실행된 가상의 테이블을 말함
- Derived Table은 사전에 정의된 SQL operation 순서를 조절 할 수 있음

SQL Operation Order
1. FROM, JOIN
2. WHERE
3. GROUP BY
4. HAVING
5. Window functions
6. SELECT
7. DISTINCT
8. UNION, UNION ALL
9. ORDER BY
10. OFFSET
11. LIMIT

CTE (Common Table Expression)
- CTE를 사용하면 현재 실행 중인 명령문에 범위가 바인딩 된 가상 테이블을 정의할 수 있음 (With 절 사용)
- Derived Table을 대체할 수 있으며, 가독성이 더 좋음
```sql
WITH 
p_pc AS (
	SELECT 
	p.id AS post_id, p.title AS post_title,
	pc.id AS comment_id, pc.review AS comment_review,
	COUNT(post_id) OVER (PARTITION BY post_id) AS comment_count
	FROM post p 
	LEFT JOIN post_comment pc ON p.id = pc.post_id
	WHERE p.title LIKE '%SQL%'
),
p_pc_r AS (
	SELECT 
	post_id, post_title, comment_id, comment_review,
	DENSE_RANK() OVER (ORDER BY p_pc.comment_count DESC) AS ranking
	FROM p_pc
)
SELECT *
FROM p_pc_r
WHERE p_pc_r.ranking <= 2 
ORDER BY post_id, comment_id
```

### Recursive CTE
- 점진적으로 여러번 반복하여 result set을 만들 수 있음
- 계층적인 테이블 구조를 처리할 때 종종 사용되는 방식
```java
List<Map<String, Integer>> tuples = new ArrayList<>();

for (int i = 0, sum = 0; i <= 5; i++) {
	Map<String, Integer> tuples = new HashMap<>();

	tuple.put("i",i);
	tuple.put("consecutive_sum", sum += i);

	tuples.add(tuple)
}
```

```sql
WITH RECURSIVE
	sonecutive_number_sum (i, consecutive_sum)
AS (
	SELECT 0, 0
	UNION ALL 
	SELECT i + 1, (i + 1) + consecutive_sum
	FROM consecutive_number_sum
	WHERE i < 5
)
SELECT i, consecutive_sum
FROM consecutive_number_sum
```

대댓글이 가능하다고 할 때, 좋아요 순 3순위 안의 댓글들을 들고 오려고 할 때 다음과 같이 짤 수 있음
```sql
WITH RECURSIVE post_comment_score(id, root_id, post_id, parent_id, review, created_on, score) AS (
	SELECT id, id, post_id, parent_id, review, created_on, score
	FROM post_comment
	WHERE post_id = 1 AND parent_id IS NULL
	UNION ALL 
	SELECT pc.id, pcs.root_id, pc.post_id, pc.review, pc.created_on, pc.score
	FROM post_comment pc
	INNER JOIN post_comment_core pcs ON pc.parent_id = pcs.id
),
total_score_comment AS (
	SELECT id, parent_id, review, created_on, score, SUM(score) OVER (PARTITION BY root_id) AS total_score
	FROM post_commnet_score
),
total_score_ranking AS (
	SELECT id, parent_id, review, created_on, score, total_score, DENSE_RANK() OVER (ORDER BY total_score DESC) AS ranking
	FROM total_score_comment
)
SELECT id, parent_id, review, created_on, score, total_score
FROM total_score_ranking
WHERE ranking <= 3
ORDER BY total_score DESC, id ASC
```

Time of application-level processing vs database (hierarchical data)
- 데이터가 적은 경우 : 시간이 거의 엇비슷
- 데이터가 많은 경우 : database에서 처리하는 것이 시간이 더 빠르다.