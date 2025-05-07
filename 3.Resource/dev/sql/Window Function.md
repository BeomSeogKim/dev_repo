- 집계함수 (Aggregate Function)처럼 동작하지만, 행들을 그룹으로 묶지 않고도 집계 결과를 각 행에 함께 표시할 수 있도록 해주는 함수
- 일반적인 집계 함수와 유사하나, 결과가 집계된 하나의 행으로 줄어들지 않고, 각 행에 계산된 값을 추가함

기본 구조
```sql
<Window Function> OVER (
	[PARTITION BY Column]
	[ORDER BY Column]
	[ROWS BETWEEN ...]
)
```

| 구성 요소        | 설명                                 |
| ------------ | ---------------------------------- |
| OVER         | 윈도우 함수를 사용할 때 반드시 필요하며 윈도우의 범위를 정의 |
| PARTITION BY | 데이터를 파티션 (논리적 그룹)으로 나눔             |
| ORDER BY     | 파티션 내에서 행의 순서를 지정                  |
| ROWS BETWEEN | 현재 행을 기준으로 어느 범위의 데이터를 볼 지 지정      |

### Window Function
#### Aggregate Function
| AVG( )   | 평균 값 반환 |
| -------- | ------- |
| COUNT( ) | 건 수 반환  |
| MAX( )   | 최대 값 반환 |
| MIN( )   | 최소 값 반환 |
| SUM( )   | 합계 값 반환 |
#### Non-Aggregate Function
| RANK ( )      | 랭킹 값 반환 (Gap 존재)                     |
| ------------- | ------------------------------------ |
| DENSE_RANK( ) | 랭킹 값 반환 (Gap 없음)                     |
| LAG( )        | 파티션 낸에서 파라미터(N)을 이용해 N번째 이전 레코드 값 반환 |
| LAST_VALUE( ) | 파티션의 마지막 레코드 값 반환                    |
| LEAD( )       | 파티션 내에서 파라미터(N)을 이용해 N번째 이후 레코드 값 반환 |
| NTH_VALUE( )  | 파티션의 n번째 값 반환                        |
| NTILE         | 파티션별 전체 건수를 파라미터(N)로 N-등분한 값         |

### Range 관련 함수 

Maximum Frame
- 기본 값이며 전체 파티션을 참조
- 각 행을 기준으로 현재 행까지 전체 누적 집계를 수행
```sql
ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
```

Specific Frame
- 프레임의 시작과 끝점을 명시적으로 지정하는 모드 
- ROWS는 물리적 행 수, RANGE는 값의 차이를 기준으로 함
```sql
SUM(amount) OVER (
	ORDER BY order_date
	ROWS BETWEEN 2 PRECEDING AND 2 FOLLOWING
)
```

Groups Mode
- ORDER BY로 정렬된 값이 같은 행들을 하나의 그룹으로 간주하고, 해당 그룹 기준으로 프레임을 지정
```sql
SUM(score) OVER (
	ORDER BY score
	GROUPS BETWEEN 1 PRECEDING AND CURRENT ROW
)
```

Range Mode
- 정렬 기준 컬럼 값의 범위를 지정해 프레임을 구성 
```sql
SUM(amount) OVER (
  ORDER BY transaction_date
  RANGE BETWEEN INTERVAL '7' DAY PRECEDING AND CURRENT ROW
)
```