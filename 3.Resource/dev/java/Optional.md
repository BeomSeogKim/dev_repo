### 필요한 이유
- NullPointerException
	- null 체크 누락 시, null 참조에 대해 메서드를 호출 했을 때 NPE 문제 발생
- 가독성 저하
	- null을 반환하거나 사용한다면, 코드 작성히마다 분기처리를 해야 하여 가독성이 떨어짐
- 의도가 드러나지 않음
	- 해당 메서드가 null을 반환할 수도 있다는 사실을 명확히 알기가 어려움

```java
public final class Optional<T> {
	private final T value;
}
```

### Constructor
- Optional.of(T value)
	- 내부 값이 확실하게 null이 아닐 때 사용.
	- 만약 value가 null이라면 NPE 발생
- Optional.ofNullable(T value)
	- 내부 값이 null 일 수도 있고, 아닐 수도 있을 때 사용
	- 만약 value가 null이라면 Optional.empty() 반환
- Optional.empty()
	- 값이 없을 때 생성하는 방식

### 값 획득
- isPresent(), isEmpty()
	- Optional에 값이 있는 지 여부를 검사하는 메서드
- get()
	- 값이 있는 경우 Optional이 담고 있는 값을 반환
	- 만약 값이 없다면 NoSuchElementException 발생
	- ***사용 지양***
- orElse(T other)
	- 값이 있다면 값을 반환
	- 값이 없다면 other를 반환
- orElseGet(Supplier< ? extends T> supplier)
	- 값이 있다면 값을 반환
	- 값이 없다면 supplier를 호출하여 생성된 값 반환
- orElseThrow(...)
	- 값이 있다면 값을 반환
	- 값이 없다면 지정한 예외를 던짐

### 값 처리
- ifPresent(Consumer< ? extends T> action)
	- 값이 존재하면 action 실행
	- 값이 없으면 실행 X
- ifPresentOrElse(Consumer< ? extends T> action, Runnable emptyAction)
	- 값이 존재하면 action 실행
	- 값이 없으면 emptyAction 실행
- map(Function< ? super T, ? extends U> mapper)
	- 값이 있으면 mapper를 적용한 결과 Optional< U > 를 반환
	- 값이 없으면 Optional.empty() 반환
- flatMap(Function< ? super T, ? extends Optional< ? extends U>> mapper)
	- map과 유사하지만, Optional 반환 시 중첩되지 않고 평탄화하여 반환
- filter(Predicate< ? super T> predicate)
	- 값이 있고 조건을 만족하면 그대로 반환
	- 조건을 만족하지 않거나 값이 없다면 Optional.empty() 반환

### 즉시 평가 vs 지연 평가
- 즉시 평가 (Eager evaluation)
	- 값을 바로 생성하거나 계산해버리는 것
- 지연 평가 (Lazy evaluation)
	- 값이 실제로 필요할 때까지 계산을 미루는 것