> 람다는 함수형 프로그래밍을 지원하기 위한 핵심 기능 
> 람다는 익명함수이다.

람다의 기본 표현식
(매개변수) -> {본문}

람다는 익명함수를 보다 간편하게 작성할 수 있도록 지원한다.
-> 보일러플레이트 코드를 크게 줄일 수 있음
```java
interface Procedure {
   void run();
}


public static void main(String[] args) {

	// 익명 클래스 사용 방식
	Procedure procedure1 = new Procedure() {
		@Override
		public void run() {
			System.out.println("Hello!");
		};
	};

	// 람다 사용 방식
	Procedure procedure2 = () -> {System.out.println("Hello!");};

}
```

### 함수형 인터페이스
> 정확히 하나의 추상 메서드를 가지는 인터페이스
> 람다는 함수형 인터페이스에만 할당이 가능하다.

함수형 인터페이스는 어노테이션과 함께 명시

```java
@FunctionalInterface
public interface SamInterface {
	void run();
}
```

### 람다와 시그니처
람다를 함수형 인터페이스에 할당할 때는 메서드 시그니처가 일치해야 한다. 
- 