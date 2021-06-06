스프링 프로젝트의 중심이자 핵심인 스프링 코어 (Spring core) 에 대해 살펴본다.
스프링 코어 중에서도 특히 중요한 것은 DI (Dependency Injection) 와 AOP (Aspect Oriented Programming) 다. 

## DI
보통 엔터프라이즈 어플리케이션을 개발할 때는 하나의 처리를 수행하기 위해 여러 개의 컴포넌트를 조합해서 구현한다. 컴포넌트에는 '공통으로 사용되는 기능 컴포넌트', '데이터베이스에 접근하기 위한 컴포넌트', '외부 시스템이나 서비스에 접속하기 위한 컴포넌트' 등 다양한 컴포넌트가 있다. 하나의 처리를 구현하기 위해 여러 개의 컴포넌트를 통합할 때 의존성 주입이라는 접근 방식이 큰 힘을 발휘한다. 

어떤 클래스가 필요로 하는 컴포넌트를 외부에서 생성한 후, 내부에서 사용 가능하게 만들어 주는 과정을 '의존성 주입(DI)한다' 또는 '인젝션(Injection) 한다' 라고 말한다. 그리고 이러한 의존성 주입을 자동으로 처리하는 기반을 'DI 컨테이너' 라고 한다. 

스프링 프레임워크가 제공하는 기능 중 가장 중요한 것이 DI 컨테이너 기능이다. 

DI 컨테이너를 통해 각 컴포넌트의 인스턴스를 생성하고 통합 관리하면서 얻을 수 있는 장점은 컴포넌트 간의 의존성 해결 뿐만 아니라 인스턴스 스코프 관리도 DI 컨테이너가 대신한다. 또 각 인스턴스가 필요로 하는 공통 처리 코드를 외부에 자동으로 끼워넣는 AOP 기능도 DI 컨테이너가 대신한다. 

DI 는 의존성 주입이라고하며, IoC 라고 하는 소프트웨어 디자인 패턴이다. IoC 는 인스턴스를 제어하는 주도권이 역전된다는 의미다. 컴포넌트를 구성하는 인스턴스의 생성과 의존 관계의 연결 처리를 해당 소스코드가 아닌 DI 컨테이너에서 대신해주기 때문에 제어가 역전됐다고 한다. 

DI 컨테이너를 활용하면 인스턴스를 어플리케이션에서 직접 생성해서 쓰는 방법 대신 DI 컨테이너가 만들어주는 인스턴스를 가져오는 방법을 사용할 수 있다. 이 때 취득한 인스턴스가 의존하는 또 다른 인스턴스 역시 DI 컨테이너에서 관리되기 때문에 연쇄적으로 의존성 주입이 발생해서 연관된 클래스의 인스턴스 모두를 사용할 수 있게 된다. 

DI 컨테이너에서 인스턴스를 관리하는 방법의 장점 : 
- 인스턴스 스코프를 제어할 수 있다.
- 인스턴스 생명 주기를 제어할 수 있다.
- AOP 방식으로 공통 기능을 집어넣을 수 있다.
- 의존하는 컴포넌트 간의 결합도를 낮춰서 단위 테스트하기 쉽게 만든다.

## ApplicationContext 와 빈 정의
스프링 프레임워크에서는 ApplicationContext 가 DI 컨테이너의 역할을 한다. 

@Configuration 과 @Bean 어노테이션을 사용해서 DI 컨테이너에 컴포넌트를 등록하면 어플리케이션은 DI 컨테이너에 있는 Bean 을 ApplicationContext 인스턴스를 통해 가져올 수 있다. 스프링 프레임워크에서는 DI 컨테이너에 등록하는 컴포넌트를 빈이라고 하고, 빈에 대한 설정 정보를 빈 정의 (Bean Definition) 이라고 한다. DI 컨테이너에서 빈을 찾아오는 행위를 룩업(lookup) 이라고 한다.

### DI 컨테이너에서 빈 가져오기
|        방법        |예                         |
|----------------|-------------------------------|
|가져오려는 빈의 타입을 지정하는 방법. 지정한 타입에 해당하는 빈이 DI 컨테이너에 오직 하나만 있을 때 사용| UserService userService = context.getBean(UserService.class);
|가져오려는 빈의 이름과 타입을 지정하는 방법. 지정한 타입에 해당하는 빈이 DI 컨테이너에 여러 개 있을 때 이름으로 구분하기 위해 사용. | UserService userService = context.getBean("userService", UserService.class);
|가져오려는 빈의 이름을 지정하는 방법. | UserService userService = (UserService) context.getBean("userService");

### 대표적인 빈 설정 방법
|        방법        |설명                         |
|----------------|-------------------------------|
|자바 기반 설정 방식 | 자바 코드로 빈을 설정. 자바 클래스에 @Configuration 어노테이션을 메소드에 @Bean 어노테이션을 사용해 빈을 정의하는 방법. 특히 스프링 부트에서 많이 활용된다.
|XML 기반 설정 방식 | XML 파일을 사용하는 방법으로 <bean> 요소의 class 속성에 자바에서 패키지에 클래스명까지 붙여 쓴 완전한 클래스 이름을 기술하면 빈이 정의된다. 
|어노테이션 기반 설정 방식 | @Component 같은 마커 어노테이션이 부여된 클래스를 탐색해서 (Component Scan) DI 컨테이너에 빈을 자동으로 등록하는 방법. DI 컨테이너에 관리할 빈을 빈 설정 파일에 정의하는 대신 빈을 정의하는 어노테이션을 빈의 클래스에 부여하는 방식을 사용. 해당 어노테이션이 붙은 클래스를 탐색해서 DI 컨테이너에 자동으로 등록하는데 이런 탐색 과정을 컴포넌트 스캔이라고 한다. 의존성 주입도 어노테이션이 붙어 있으면 DI 컨테이너가 자동으로 필요로 하는 의존 컴포넌트를 주입한다. 이런 주입 과정을 오토와이어링이라 한다. 

### ApplicationContext 생성 방법
|        방법        |설명                         |
|----------------|-------------------------------|
|자바 기반의 설정 방식. AnnotationConfigApplicationContext 생성자에 @Configuration 어노테이션이 붙은 클래스를 인수로 전달.| ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
|어노테이션 기반의 설정 방식. AnnotationConfigApplicationContext 생성자에 패키지명을 인수로 전달. 지정된 패키지 이하의 경로에서 컴포넌트를 스캔. | ApplicationContext context = new AnnotationConfigApplicationContext("com.example.app");
|XML 기반의 설정방식. ClassPathXmlApplicationContext 생성자에 XML 파일을 인수로 전달. 경로에 접두어가 생략된 경우 클래스패스 안에서 상대 경로로 설정 파일을 탐색. | ApplicationContext context = new ClassPathXmlApplicationContext("META-INF/spring/applicationContext.xml");
|XML 기반의 설정 방식으로 FileSystemXmlApplicationContext 의 생성자에 XML 파일을 인수로 전달. 경로에 접두어가 생략된 경우 JVM 작업 디렉터리 안에서 상대 경로로 설정 파일 탐색.

ApplicationContext 단독 어플리케이션에서 스프링 프레임워크를 사용하거나 
JUnit 으로 만든 테스트 케이스 안에서 스프링 프레임워크를 구동할 때 사용된다. 반면 **웹 어플리케이션에서는 스프링 MVC 를 활용하게 되는데, 이 때 ApplicationContext 를 웹 환경에 맞게 확장한 WebApplicationContext 를 사용한다.**


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk1NTc3MjI2OSwtMTg2Mzk2MzU1OSwtMT
Y5NDcyNjYxNCwxMTQwODU2ODA5LDE1ODk0ODA3NzAsMTk1ODAx
MDkyMSwxODE5NzgzNjk4LDE0NDkyNjM0ODFdfQ==
-->