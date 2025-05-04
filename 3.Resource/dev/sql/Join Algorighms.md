JOIN을 하는 것에 있어 3가지의 알고리즘이 존재함
1. Nested Loops
2. Hash Join
3. Merge Join

### Nested Loops
이중 중첩문 구조로 Join하여 탐색하는 방식
Time Complexity : O(N x M)
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

### Hash Join
메모리 기반 table 구조에 저장해두고 사용하는 방식 
Time Complexity : O (N + M)

**Step1**  : 상대적으로 적은 요소들을 가진 table의 record를 hash table에 저장 (key : join attribute)
```java
Map<Long, Student> studentMap = new HashMap<>();

for (Student student : stduents) {
	studentMap.put(student.getId(), student);
}
```

**Step2** : 많은 요소를 가진 table을 순회하며 만족하는 결과들을 수집
```java
List<Tuple> tuples = new ArrayList<>();

for (StduentGrade studentGrade : studentGrades) {
	Long studentId = studentGrade.getStudentId();
	Student student studentMap.get(studentId);

	if (student != null) {
		tuples.add(
			new Tuple()
				.add("first_name", student.getFirstName())
				.add("last_name", studnet.getLastName())
				.add("grade", stduentGrade.getGrade());
		)
	}
}
```

### Merge Join
