- 자바 8부터 추가된 기능으로, 데이터의 흐름을 추상화해서 다루는 도구
- Collection, 배열 등의 요소들을 **연산 파이프라인**을 통해 연속적인 형태로 처리할 수 있게 함
	- 여러 연산을 체이닝하여 데이터를 변환, 필터링 계산하는 구조.
- 특징
- Immutable 
	- 원본을 변경하지 않고 결과만 새로 생성 함
- 일회성
	- 한번 소비된 스트림은 다시 사용 불가능하다. 
	- 만약 필요하다면 스트림을 새로 생성해야함
- 파이프라인 구성
	- 중간 연산들이 이어지다가, 최종 연산을 만나면 연산이 수행되고 종료됨
- 지연 연산
	- 중간 연산은 필요할 떄 까지 실제로 동작하지 않고, 최종 연산이 실행될 때 한번에 처리됨
- 병렬처리
	- 스트림으로부터 병렬 스트림을 쉽게 만들 수 있음

#### 일괄 처리 vs 파이프라인 처리
- 일괄 처리
	- 각 연산마다 **데이터 전체**를 한번에 처리하는 방식
- 파이프라인 처리
	- 한 연산을 마칠 때 마다 다음 연산으로 넘어가는 구조

##### 단축 평가 (Short circuit)
- 조건을 만족하는 결과를 찾으면 더 이상 연산을 진행하지 않는 방식.

### 생성 방법 
| 생성 방법            | 코드 예시                         | 특징                      |
| ---------------- | ----------------------------- | ----------------------- |
| Collection       | list.stream()                 | 컬렉션에서 스트림 생성            |
| 배열               | Arrays.stream(arr)            | 배열에서 스트림 생성             |
| Stream.of(...)   | Stream.of("a", "b", "c")      | 직접 요소를 입력해 스트림 생성       |
| 무한 스트림(iterate)  | Stream.iterate(0, n -> n + 2) | 무한 스트림 생성 (초기값 + 함수)    |
| 무한 스트림(generate) | Stream.generate(Math::random) | 무한 스트림 생성 (Supplier 사용) |

### 중간 연산 
> 스트림 파이프라인에서 데이터를 가공하는 단계
> 주로 변환, 필터링, 정렬등을 한다.

| 연산        | 설명                                 | 예시                                                        |
| --------- | ---------------------------------- | --------------------------------------------------------- |
| filter    | 조건에 맞는 요소만 남김                      | stream.filter ( n -> n % 2 == 0)                          |
| map       | 요소를 다른 형태로 변환                      | stream.map(n -> n * 2)                                    |
| flatMap   | 중첩 구조 스트림을 일차원으로 평탄화               | stream.flatMap (n -> n.stream())                          |
| distinct  | 중복 요소 제거                           | stream.distinct()                                         |
| sorted    | 요소 정렬                              | stream.sorted()<br>stream.sorted(Comparator < ? super T>) |
| peek      | 중간 처리 (로그, 디버깅)                    | stream.peek(System.out::println)                          |
| limit     | 앞에서 N개의 요소만 추출                     | stream.limit(5)                                           |
| skip      | 앞에서 N개의 요소를 건너뛰고 <br>이후 요소만 추출     | stream.skip(5)                                            |
| takeWhile | 조건을 만족하는 동안 추출                     | stream.takeWile(n -> n < 5)                               |
| dropWhile | 조건을 만족하는 동안 요소를 버리고 <br>이후 요소부터 추출 | stream.dropWhile( n -> n < 5)                             |

### FlatMap
- 중첩 컬렉션을 다룰 때 유용한 중간 연산
- 각 요소를 스트림으로 변환한 뒤, 그 결과를 하나의 스트림으로 평탄화 해 줌

### 최종 연산
- 스트림 파이프라인의 끝에 호출되어 실제 연산을 수행하고 결과를 만들어냄
- 최종 연산이 실행된 후 스트림은 소모되어 더 이상 사용이 불가하다.

| 연산        | 설명                                                       | 예시                                       |
| --------- | -------------------------------------------------------- | ---------------------------------------- |
| collect   | Collector를 사용하여 결과 수집<br>(다양한 형태로 변환 가능)                 | stream.collect(Collectors.toList())      |
| toList()  | 스트림을 불변 리스트로 수집                                          | stream.toList()                          |
| toArray() | 스트림을  배열로 변환                                             | stream.toArray(Integer[]::new)           |
| forEach   | 각 요소에 대해 동작 수행<br>(반환값 X)                                | stream.forEach(System.out::println)      |
| count     | 요소 개수 반환                                                 | long count = stream.count()              |
| reduce    | 누적 함수를 사용해 <br>모든 요소를 단일 결과로 합침<br>초기값이 없으면 Optional로 반환 | int sum = stream.reduce(0, Integer::sum) |
| min / max | 최소값, 최대값을 Optional로 반환                                   | -                                        |
| findFirst | 조건에 맞는 첫 번째 요소 반환 <br>(Optional)                         | stream.findFirst()                       |
| findAny   | 조건에 맞는 아무 요소반환<br>(Optional)                             | stream.findAny()                         |
| anyMatch  | 하나라도 조건을 만족하는가? <br>(boolean)                            | stream.anyMatch(n -> n > 5)              |
| allMatch  | 모두 조건을 만족하는가? <br>(booleabn)                             | stream.allMatch(n -> n > 5)              |
| noneMatch | 하나도 조건을 만족하지 않는가?                                        | stream.noneMatch(n -> n > 5)             |