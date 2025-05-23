### Circuit Breaker의 정의 및 작동 원리
Circuit Breaker는 분산 시스템에서 **시스템 안정성**과 **장애 격리**를 위해 사용되는 설계 패턴
서비스 호출 사이에 프록시 형태의 차단기를 두어 장애가 발생할 가능성이 높은 연산을 반복하지 않도록 함으로써 시스템의 복원력을 높임
외부 서비스에서 장애가 발생했을 때, 애플리케이션이 무작정 재시도하는 것을 막고, 문제 원인이 해결될 때 까지 빠르게 실패하도록 함.
- transient(일시적 장애)에 대해서는 일정 횟수 재시도
- 영속적인 장애에 대해서는 서킷 브레이커로 전환하여 장애 전파 차단

Circuit Breaker에서의 상태 
![[State of CircuitBreaker.png]]
- Closed
- Open
- Half-Open

Closed 상태에서는 서비스 호출이 정상적으로 전달되며 실패 회수를 모니터링.
실패율이 사전에 정의된 임계값을 넘어서면 회로가 Open 상태로 전환되어 더이상의 호출을 즉시 차단하고, 곧바로 예외나 fallback을 반환

Open 상태에서는 일정 대기 시간 동안 요청을 차단해 시스템이 문제를 복구하거나 정상화할 시간을 줌.
이후 대기 기간이 지나면 Half-Open 상태로 전환되어 일부 요청만 통과시켜 서비스를 시험.

Half Open 상태에서 제한된 시도들이 모두 성공하는 경우 서비스가 복구된 것으로 간주하여 Closed 상태로 돌아가고 실패 카운터를 초기화. 만약 제한된 시도에서 하나라도 실패하면 다시 Open 상태로 돌아가 일정시간동안 호출을 막음

### Circuit Breaker의 필요성
- 부분적인 실패가 전체 시스템으로 전파되는 것을 막고, 안정적으로 서비스 품질을 유지하기 위함.

이점
- 실패 전파 방지 및 장애 격리
	- 하위 서비스에 장애가 발생해도, 서킷 브레이커가 해당 호출을 차단함으로써, 문제가 다른 서비스로 전이되지 않도록 방지.
	- 한 구성 요소의 실패로 전체 시스템이 무너지는 도미노 효과 방지
- 시스템 자원 보호 및 안정성 향상
	- 장애 상태의 서비스를 무작정 기다리거나, 계속 호출하면 스레드, 메모리 같은 자원이 쌓여 고갈 될 수 있음
	- fail-fast 전략으로 불필요한 대기를 없애고, 애플리케이션이 남은 자원을 가지고 핵심 기능을 지속할 수 있도록 함
- Graceful Degradation
	- 서킷 브레이커 동작 중에는 Fallback 경로를 제공해 사용자가 최소한의 기능이라도 이용할 수 있게 함
	- Open 상태에서 미리 정의된 기본 값 혹은 캐시된 응답을 반환함으로써 기능 축소 형태로 서비스를 이어간다던지 하는 방식
- 자가 진단 및 회복 전략
	- Half-Open 상태에서 자동으로 서비스 상태를 재검증하여, 장애 원인이 해결되면 정상 상태로 복귀함
	- 오퍼레이터가 개입하지 않아도 시스템이 자체 치유를 할 수 있음
	- 서킷 상태 변화 이벤트를 로그/모니터링 하여 서비스 건강 상태를 실시간으로 파악하고 alert을 울릴 수도 있음

### Hystrix Vs Resilience4J
**Hystrix**
- Netflix에서 개발한 Circuit Breaker 라이브러리
- 2018 이후 유지보수 중단
- 자체 스레드 풀 격리 방식으로 안정성 확보
- 설정과 사용이 간단하나 유연성이 부족함
- Servo 기반 메트릭 시스템
- Spring Cloud Netflix로 통합 사용
- Java 6이상 사용 가능
- Spring 공식 문서에서 비권장
Resilience4J
- Hystrix의 대안으로 개발된 모던 라이브러리
- Java8+ 함수형 스타일 지원
- 경량형 모듈형 구조 (CircuitBreaker, Retry, RateLimiter)
- 현재 활발히 유지보수 중
- 스레드 풀 대신 호출 스레드 내 처리 
- Micrometer와 자연스럽게 통합 가능
- Spring 공식 문서에서 권장 
