![[Statement LifeCycle.png]]
Statement의 생명주기는 다음과 같은 구조를 가짐

SQL은 선언적 언어이다
- 어떤 데이터를 읽어야 하는지 명시함
- 어떻게 읽어와야하는 지에 대해서 명시하는 것이 아님
SQL은 많은 구문으로 이루어져 있다. (SELECT, FROM, WHERE .. )
그리고 그 구문은 사전에 정의된 순서대로 실행이 된다.

Operation Order
1. FROM and JOIN
	- FROM : 어떤 소스에서부터 데이터를 가져와야 하는 지 명시
	- JOIN : FROM에 명시된 데이터 소스와 다른 데이터 소스를 결합하는 것
	 - 이 때, 다른 데이터 소스의 경우 물리적일 수도 있고, 가상일 수도 있다.
2. WHERE
	- 관심있는 데이터를 뽑아내기 위해 filter를 하는 구문
	- WHERE 구문의 경우 먼저 선행 된 FROM 에서 정의된 alias만 참조해서 쓸 수 있음
3. GROUP BY
	- GROUP BY 구문의 규칙으로 응집시킬 수 있음
	- SELECT 구문에서 aggregation function을 적용하는 것 과 같음
	- Stream Aggregate
		- 정렬 기반 집계 방식
		- 입력 데이터가 GROUP BY 키로 정렬되어있어야 함
	- Hash Aggregate
		- 해시 테이블을 이용해 GROUP BY 키로 데이터를 분류
		- 정렬이 필요하지 않으며 순서에 상관없이 집계 가능
4. HAVING
	- 두번째의 WHERE 구문처럼 작동함.
	- GROUP BY가 WHERE 절 보다 먼저 실행되기에, result set에 대해서 필터를 할 수 없음
	- HAVING에서 그런 역할을 수행
5. Window Function
	- Having 없이 행 파티션에 걸쳐 집계 함수를 적용하여 파티션 행을 단일 레코드로 줄일 수 있음
6. SELECT
	- 마지막 result set에서 필요한 데이터 프로젝션을 정의하는 것
7. DISTINCT
	- 많은 데이터베이스들이 두가지 단계를 통해서 실행됨
	- 1. result set 정렬
	- 2. 순회를 하면서 중복된 값들을 제거
8. UNION UNION ALL
	- 두개의 쿼리 결과들을 합쳐주는 역할을 함
	- UNION : 중복 제거 없이 합쳐줌
	- UNION ALL : 중복 제거
9. ORDER BY 
	- 결과를 정렬하는 순서를 명시하는 구문
	- ASC / DESC 둘다 가능
10. OFFSET
11. LIMIT, FETCH ROWS, TOP
