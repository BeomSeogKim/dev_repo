MySQL 5.7.8 부터 도입된 네이티브 JSON 데이터 타입
- 구조화된 데이터를 효율적으로 저장하고 조회할 수 있음
- 일반적인 문자열 저장 방식과 달리, 실제 파싱 가능한 JSON 형식을 강제하며, 다양한 내장 함수 및 최적화 제공

| 특징     | 설명                                               |
| ------ | ------------------------------------------------ |
| 저장 방식  | 내부적으로 Binary JSON 포맷으로 저장되어 빠른 파싱 및 검색 가능        |
| 유효성 검사 | 저장 시 JSON 형식이 아니면 오류 발생                          |
| 가변 타입  | 배열, 객체, 숫자, 문자열 등 JSON 타입 그대로 저장 가능              |
| 함수 지원  | JSON관련된 다양한 함수 제공                                |
| 인덱싱    | JSON 전체에 대한 인덱스는 불가하나, 가상컬럼 + 인덱스를 조합해 부분 인덱싱 가능 |

### 사용 예시
테이블 생성 
```sql
CREATE TABLE user_profiles (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(100),
  attributes JSON
);
```

데이터 삽입
```sql
INSERT INTO user_profiles (name, attributes)
VALUES ('Alice', '{"age": 30, "hobbies": ["reading", "gaming"]}');
```
JSON 값 추출 
```sql
-- 나이 조회
SELECT JSON_EXTRACT(attributes, '$.age') AS age FROM user_profiles;

-- hobbies 배열의 첫 번째 항목
SELECT JSON_EXTRACT(attributes, '$.hobbies[0]') FROM user_profiles;

-- 단축 문법 (MySQL 5.7.22 이상)
SELECT attributes->'$.age' FROM user_profiles;
```

JSON 값 수정 (부분 업데이트)
```sql
-- age 값 수정
UPDATE user_profiles
SET attributes = JSON_SET(attributes, '$.age', 31)
WHERE name = 'Alice';

-- hobbies 배열에 값 추가
UPDATE user_profiles
SET attributes = JSON_ARRAY_APPEND(attributes, '$.hobbies', 'cycling')
WHERE name = 'Alice';
```

JSON 인덱싱 (가상 컬럼 활용)
```sql
ALTER TABLE user_profiles
ADD COLUMN age INT GENERATED ALWAYS AS (JSON_UNQUOTE(attributes->'$.age')) STORED,
ADD INDEX idx_age (age);
```

### JSON 함수 요약

| **함수**                            | **설명**        |
| --------------------------------- | ------------- |
| JSON_EXTRACT(json, path)          | 특정 경로 값 추출    |
| JSON_SET(json, path, val)         | 기존 값 수정 또는 추가 |
| JSON_REMOVE(json, path)           | 특정 값 제거       |
| JSON_ARRAY(val1, val2, ...)       | 배열 생성         |
| JSON_OBJECT(key1, val1, ...)      | 객체 생성         |
| JSON_MERGE_PRESERVE(json1, json2) | JSON 병합       |
| JSON_CONTAINS(json, val [, path]) | 포함 여부 확인      |
### 장단점 요약
장점
- 