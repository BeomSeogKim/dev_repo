![[FrontController.png]]
- FrontController에서 공통적인 로직들을 처리
	- ex) 인증, 로깅 등
- FrontController는 공통적인 로직들을 처리한 후 담당 핸들러로 *매핑*해준다.
- Spring에서는 DispatcherServlet이 FrontController역할을 한다.