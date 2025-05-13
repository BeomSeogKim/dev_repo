- Java 기반 웹 애플리케이션에서 Servlet을 실행하고 관리하는 서버 측 컴포넌트

**Servlet Container 생성**
```java
ServletWebServerFactory serverFactory = new TomcatServletWebServerFactory();
WebServer webServer = serverFactory.getWebServer();
webServer.start();
```
- ServletWebServerFactory의 구현체를 통해서 ServletContainer를 생성할 수 있다.
	- 구현체로는 Jetty, Tomcat, UnderTow 등이 있다.

**Servelt 등록**
- Servlet을 등록하기 위해서는 ServletContext가 필요하다.
- 등록의 경우 getWebServer에서 ServletContextInitializer 구현체를 넣어주면 된다.