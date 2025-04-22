스트림의 중간 연산을 거쳐, 최종 연산으로써 데이터 처리 시, 결과물을 나타내기 위해 사용함

#### Collectors의 주요 기능
| 기능       | 메서드 예시                                | 설명                                                             | 반환 타입     |
| -------- | ------------------------------------- | -------------------------------------------------------------- | --------- |
| List로 수집 | toList()<br>toUnmodifiableList()      | 스트림의 요소를 List로 모음<br>toUnmodifiableList() : 불변 리스트             | List< T > |
| Set으로 수집 | toSet()<br>toCollection(HashSet::new) | 스트림의 요소를 Set으로 모음<br>특정 Set 타입으로 모으려는 경우 <br>toCollection() 사용 | Set< T >  |
| Map으로 수집 | toMap(keyMapper, valueMapper)         | 스트림 요소를 Map의 형태로 수집<br>중복 키가 생길 경우 mergeFuncion으로 해결하고         |           |
|          |                                       |                                                                |           |
|          |                                       |                                                                |           |
|          |                                       |                                                                |           |
|          |                                       |                                                                |           |
|          |                                       |                                                                |           |
|          |                                       |                                                                |           |
|          |                                       |                                                                |           |
|          |                                       |                                                                |           |
|          |                                       |                                                                |           |