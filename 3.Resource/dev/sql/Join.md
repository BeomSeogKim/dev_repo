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