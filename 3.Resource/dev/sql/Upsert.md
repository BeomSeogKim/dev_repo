- 같은 UNIQUE 컬럼 값에 대해 행이 없는 경우 INSERT, 행이 있는 경우 UPDATE를 하는 방식
- SQL:2003표준부터는 MERGE 키워드를 사용하여 UPSERT를 모방할 수 있음
- PostgreSQL, MySQL은 비표준 대안들을 제공함. 
	- ON CONFLICT, ON DUPLICATE KEY

MERGE 방식
```sql
MERGE INTO book
USING (SELECT 1 FROM dual)
ON (id = 1)
WHEN MATCHED THEN 
UPDATE SET 
	title = "edited title",
	isbn = "122-333213213"
WHEN NOT MATCHED THEN 
INSERT (
	id,
	title,
	isbn
)
VALUES (
	1,
	"title",
	"122-333213213"
)
```

PostgreSQL - ON CONFLICT
- ON CONFLICT 구문에 INSERT 혹은 UPSERT 실행문을 포함시킬 수 있음
- `DO NOTHING` 혹은 `DO UPDATE` 구문에 사용할 수 있다.
```sql
INSERT INTO book(
	id,
	title,
	isbn
)
VALUES (
	1,
	"High-Performance",
	"9200-22-22"
)
ON CONFLICT (id) DO
UPDATE SET
	title = "High-Performance 2nd",
	isbn = "1123-221-32"
```

MySQL  - ON DUPLICATE 
```sql
INSERT INTO book (
	id,
	title,
	isbn
) 
VALUES (
	1,
	"High-Performance",
	"9200-22-22"
)
ON DUPLICATE KEY 
UPDATE
	title = "High-Performance 2nd",
	isbn = "1123-221-32"
```