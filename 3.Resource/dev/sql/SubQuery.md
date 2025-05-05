> SELECT, INSERT, UPDATE, DELETE 명령문 내에 중첩된 쿼리를 말함
> sub query는 inner query라고도 불리며, sub query를 포함하는 명령문은 outer query라고 함
> sub query는 괄호로 안에 있어야 한다
> sub query는 다양한 SQL절에 중첩될 수 있음

```sql
SELECT DISTINCT
	s.id,
	s.first_name,
	s.last_name
FROM student s 
JOIN student_grade sg ON sg.student_id = s.id
WHERE sg.grade = 10
ORDER BY s.id
```

```sql
SELECT DISTINCT
	s.id,
	s.first_name,
	s.last_name
FROM student s 
WHERE EXISTS (
	SELECT 1 
	FROM student_grade sg
	WHERE sg.student_id = s.id AND sg.grade = 10
)
ORDER BY s.id
```
위 예시에서 JOIN하는 테이블을 데이터 조회용이 아닌 데이터 필터링 용
-> 이럴 경우에는 Subquery로 들고와야하는 결과를 줄이는 방식이 더 합리적이다.
- JOIN + DISTINCT
	- join을 사용해 두 테이블을 결합한 후 WHERE 조건을 적용
	- 중복 제거를 위해 DISTINCT
	- 하나의 학생이 grade = 10인 여러가지 row가 존재한다면, 그만큼 결과를 가져와서 DISTINCT
- EXISTS
	- outer query에서 student를 순회하면서, 해당 학생이 grade = 10을 갖는지 존재 여부만 확인
	- EXISTS는 첫 매칭되는 row가 있으면 바로 true, 나머지는 무시됨

### EXISTS & NOT EXISTS

Exists (subquery)
- subquery가 row를 반환하는 지 여부를 평가
- predicate
	- true : row가 반환될 때
	- false :  row가 반환되지 않을 때
- subquery는 outer query의 값들을 참조할 수 있다
- 최소 한개의 row가 return되면 더이상의 탐색을 그만 둠

Not Exists
- Exists의 반대로 동작

### IN  & NOT IN 
expression IN (subquery)
```sql
id IN (
	SELECT student_id
	FROM student_grade
	GROUP BY student_id
	HAVING AVG(grade) < 9.5
)
```
- left side의 expression과 in 절의 subquery로 평가됨
- Predicate
	- true : subquery에 있는 값이 expression과 동일 할 경우
	- false : subquery에 있는 값이 expression과 동일하지 않을 경우
- ***subquery 혹은 exrepssion이 null일 경우 비교를 하면 false가 아닌 NULL이 반환됨*** 

### ANY(SOME)
expression ANY (subquery)
expression SOME (subquery)
row_constructor ANY (subquery)
row_constructor SOME (subquery)

서브쿼리가 반환하는 값드로가 왼쪽 표현식을 비교할 때 사용됨
Predicate
- true : subquery 중 expression과 같은 것이 최소 하나라도 있을 때
- false : subquery가 아무 row도 반환하지 않거나, 하나도 일치하지 않을 경우