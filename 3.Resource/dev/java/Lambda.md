> 람다는 함수형 프로그래밍을 지원하기 위한 핵심 기능 
> 람다는 익명함수이다.

람다의 기본 표현식
(매개변수) -> {본문}

```java
interface Procedure {
   void run();
}


public static void main(String[] args) {

	// 익명 클래스 사용 방식
	Procedure procedure1 = new Procedure() {
		@Override
		public void run() {
			System.out.
		};
	};

	// 람다 사용 방식
	Procedure procedure2 = () -> {System.out.println("Hello!");};

}
```