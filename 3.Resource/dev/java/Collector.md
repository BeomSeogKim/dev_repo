스트림의 중간 연산을 거쳐, 최종 연산으로써 데이터 처리 시, 결과물을 나타내기 위해 사용함

#### Collectors의 주요 기능
| 기능       | 메서드 예시                                                                                       | 설명                                                                                        | 반환 타입                                      |
| -------- | -------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ------------------------------------------ |
| List로 수집 | toList()<br>toUnmodifiableList()                                                             | 스트림의 요소를 List로 모음<br>toUnmodifiableList() : 불변 리스트                                        | List< T >                                  |
| Set으로 수집 | toSet()<br>toCollection(HashSet::new)                                                        | 스트림의 요소를 Set으로 모음<br>특정 Set 타입으로 모으려는 경우 <br>toCollection() 사용                            | Set< T >                                   |
| Map으로 수집 | toMap(keyMapper, valueMapper)<br>toMap(keyMapper, valueMapper<br>mergeFunction, mapSupplier) | 스트림 요소를 Map의 형태로 수집<br>중복 키가 생길 경우 mergeFuncion<br>으로 해결하고, mapSupplier로 <br>타입을 지정할 수 있음 | Map<br><K, V>                              |
| 그룹화      | groupingBy(classifier)<br>groupingBy(classifier, <br>downstreamCollector)                    | 특정 기준 함수 (classifier)에 따라 그룹별로 스트림 요소를 묶음<br>각 그룹에 대해 추가로 적용할 다운스트림 컬렉터를 지정할 수 있음         | Map<K, List< T ><br>Map<K,R>               |
| 분할       | partitioningBy(predicate)<br>partitioningBy(predicate, <br>downstreamCollector)              | predicate 결과가 true, false 두가지로 나뉘어 2개 그룹으로 분할                                             | Map<Boolean, List< T >><br>Map<Boolean, R> |
| 통계       | counting(),<br>summingInt(),<br>averagintInt(),<br>...                                       | 요소의 개수, 합계, 평균 등등을 구할 수 있음                                                                | Long, Integer, Double, ...                 |
| 리듀싱      | reducing(...)                                                                                | Collector 환경에서 요소를 하나로 합치는 연산                                                             | Optional< T >                              |
| 문자열 연결   | joining(delimeter, prefix, suffix)                                                           | 문자열 스트림을 하나로 합쳐서 연결                                                                       | String                                     |
| 매핑       | mapping(mapper, downstream)                                                                  | 각 요소를 다른 값으로 변환한 뒤 다운스트림 컬렉터로 넘김                                                          |                                            |

### DownStream Collector
- Collector의 결과물에서 추가적인 연산을 하고자 하는 작업을 명시하는 것.
![[DownStreamCollector.png]]