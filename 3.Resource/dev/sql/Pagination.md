### Seek Pagination Vs Keyset Pagination
#### Offset Pagination 
```sql 
SELECT * FROM items
ORDER BY created_at DESC
LIMIT 10 OFFSET 100;
```
- 구현이 간단하며 특정 페이지로 곧바로 이동이 가능함
- OFFSET이 커질수록 성능 저하 발생 (인덱스를 건너뛰고 스캔)
- 중간에 데이터가 삽입 / 삭제되면 페이지 데이터가 흔들림

#### Seek / Keyset Pagination 
```sql 
-- created_at과 id 값을 기준으로 다음 페이지 조회
SELECT *
FROM items
WHERE (created_at < :last_created_at)
ORDER BY created_at DESC
LIMIT 10;
```

```sql
SELECT * FROM items
WHERE (created_at < :last_created_at)
	OR (created_at = :last_created_at AND id < :last_id)
ORDER BY created_at DESC, id DESC
LIMIT 10;
```
- 페이지가 깊어져도 성능 유지 (인덱스를 활용한 Range Scan)
- 데이터 변경에 강건함
- 특정 페이지로 바로 이동은 불가능 
- 데이터의 양이 많고 페이지 수가 많을 때 유용함