> 람다는 함수형 프로그래밍을 지원하기 위한 핵심 기능 
> 람다는 익명함수이다.

람다는 기본적으로 함수형 인터페이스에만 할당이 가능하다. 
See [[Functional Interface (함수형 인터페이스)]]

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



```

### 람다와 시그니처
람다를 함수형 인터페이스에 할당할 때는 메서드 시그니처가 일치해야 한다. 
- 매개변수의 개수와 타입
- 반환 타입

```

### Lambda Vs Anonymous Class

##### 상속 관계
- 익명 클래스는 일반적인 클래스와 같이 다양한 인터이와 클래스를 구현 혹은 상속 할 수 있음
- 람다 표현식은 함수형 인터페이스만 구현이 가능함
##### 호환성
- 익명 클래스는 예전 버전의 자바에서도 적용이 가능함
- 람다의 경우 자바 8 이전 버전에서는 사용이 불가함
##### this
- 익명 클래스 내부 : this 는 익명 클래스 자신을 가리킴. (외부 클래스와 별도의 컨텍스트)
- 람다 클래스 내부 : 람다 클래스를 선언한 인스턴스를 가리킴.
##### Capturing
- 익명 클래스, 람다 모두 외부 변수에 접근 할 수 있음, 다만 지역 변수는 반드시 final 혹은 effectively final

