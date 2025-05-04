JOIN을 하는 것에 있어 3가지의 알고리즘이 존재함
1. Nested Loops
2. Hash Join
3. Merge Join

### Nested Loops
이중 중첩문 구조로 Join하여 탐색하는 방식
```java
List<Tuple> tuples = new ArrayList<>();

for (Student student : students) {
	for (StudentGrade studentGrade : studentGrades) {
		if (student.getId().equals(studentGrade.getStudentdId())) {
			tuples.add(
				new Tuple()
					.add("first_name", student.getFirstName())
					.add("last_name", student.getLastName())
					.add("grade", studentGrade.getGrade())
			)
		}
	}
}
```

