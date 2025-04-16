> 정확히 하나의 추상 메서드를 가지는 인터페이스
> 람다는 함수형 인터페이스에만 할당이 가능하다.

함수형 인터페이스는 어노테이션과 함께 명시

```java
@FunctionalInterface
public interface SamInterface {
	void run();
}
```

### 자바에서 기본으로 제공하는 함수형 인터페이스 
| 인터페이스              | 메서드 시그니처          | 입력  | 출력      | 대표 사용 예시        |
| ------------------ | ----------------- | --- | ------- | --------------- |
| Function<T, R>     | R apply(T t)      | T   | R       | 데이터 변환, 필드 추출 등 |
| Consumer< T >      | void accept(T t)  | T   | -       | 로그 출력, DB 저장 등  |
| Supplier < T >     | T get()           | -   | T       | 객체 생성, 값 반환     |
| Runnable           | void run ()       | -   | -       | 스레드 실행          |
| Predicate< T >     | boolean test(T t) | T   | boolean | 조건 검사, 필터링      |
| UnaryOperator< T > | T apply(T t)      |     |         |                 |
|                    |                   |     |         |                 |
