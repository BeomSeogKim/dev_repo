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