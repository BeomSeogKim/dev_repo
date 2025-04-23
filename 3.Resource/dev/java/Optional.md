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
- Optional.ofNul
