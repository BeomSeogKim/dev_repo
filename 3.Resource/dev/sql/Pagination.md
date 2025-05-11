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
SELECT *
FROM items
WHERE (created_at < :last_created)
```