### 애플리케이션 로직 빈
- 애플리케이션 비즈니스 로직을 담고 있는 클래스로 만들어지는 빈.
- Component Scanner에 의해서 빈 구성 정보가 생성되고, 빈 오브젝트로 등록됨

### 애플리케이션 인프라스트럭처 빈
- 빈 구성 정보에 의해 컨테이너에 등록되는 빈
- 애플리케이션이 동작하는데 꼭 필요한 기술 기반을 제공하는 빈
- e.g) ServletWebServerFactory, DispatcherServlet ... 

### 컨테이너 인프라스트럭처 빈
- 스프링 컨테이너의 기능을 확장해 빈의 등록과 생성, 관계 설정, 초기화 등의 작업에 참여하는 빈
- 개발자가 작성한 구성 정보에 생성되는 것이 아닌, 컨테이너가 직접 만들고 관리하는 빈
- e.g) ApplicationContext, Environment, BeanPostProcessor ... 
