SELECT 절에서 어떤 Column들을 가져올 지 정의하는 것을 의미한다.
```sql
SELECT user.id, user.name FROM user;
```
위 쿼리에서는 user 테이블에서 id, name만 투영한 결과를 리턴함.

#### Importance
1. 불필요한 데이터 제거 : 필요한 컬럼만 가져오므로, 네트워크 / 메모리 효율이 좋음
2. DTO 매핑 : Application에서 projection이 DTO와 연결되어 특정 컬럼만 매핑 가능
3. 성능 최적화 : SELECT * 는 모든 컬럼을 가져오므로, JOIN이 많을 경우 성능이 나빠질 수 있음