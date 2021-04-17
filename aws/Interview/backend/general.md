## 언어 관련

### Java

JVM의 구조와 Java의 실행방식을 설명해주세요.

GC가 무엇인지, 필요한 이유는 무엇인지, 동작방식에 대해 설명해주세요.

컬렉션 프레임워크에 대해서 설명해주세요.

제네릭에 대해서 설명해주세요.

애노테이션에 대해서 설명해주세요.

오버라이딩과 오버로딩이 무엇이며 어떤 차이가 있을까요?

인터페이스와 추상클래스의 차이점에 대해 설명해주세요.

클래스는 무엇이고 객체는 무엇인가요?

정적(static)이란 무엇인가요?

자바의 원시타입들은 무엇이 있으며 각각 몇 바이트를 차지하나요?

접근 제어자의 종류와 이에 대해 설명해주세요.

객체지향에 대해서 설명해주세요.

SOLID(객체지향 5대원칙)에 대해서 설명해주세요.

동일성(identity)와 동등성(equality)에 대해 설명해주세요. (equals(), ==)

원시타입과 참조타입의 차이에 대해 설명해주세요.

String, StringBuilder, StringBuffer 각각의 차이에 대해 설명해주세요.

Checked Exception과 Unchecked Exception에 대해 설명해주세요. 

스프링 트랜잭션 추상화에서 rollback 대상은 무엇일까요?

Java8에서 추가된 기능에 대해서 설명해주세요.try-with-resource에 대해서 설명해주세요.

강한 결합과 느슨한 결합이 무엇인지 설명해주세요.

직렬화와 역직렬화에 대해서 설명해주세요.

자바의 동시성 이슈(공유자원 접근)에 대해 설명해주세요.

Mutable 객체와 Immutable 객체의 차이점에 대해 설명해주세요.

자바에서 null을 안전하게 다루는 방법에 대해 설명해주세요.

### Spring

Spring DI/IoC는 어떻게 동작하나요?

Spring Bean이란 무엇인가요?

스프링 Bean의 생성 과정을 설명해주세요.

스프링 Bean의 Scope에 대해서 설명해주세요.

IoC 컨테이너의 역할은 무엇이 있을까요?

DI 종류는 어떤것이 있고, 이들의 차이는 무엇인가요?

Autowiring 과정에 대해서 설명해주세요.

Spring Web MVC의 Dispatcher Servlet의 동작 원리에 대해서 간단히 설명해주세요.

프론트 컨트롤러 패턴이란 무엇인가요?

Servlet Filter와 Spring Interceptor의 차이는 무엇인가요?

Spring에서 CORS 에러를 해결하기 위한 방법을 설명해주세요.

Bean/Component 어노테이션에 대해서 설명해주시고, 둘의 차이점에 대해 설명해주세요.

POJO란 무엇인가요? 

Spring Framework에서 POJO는 무엇이 될 수 있을까요?

Spring Web MVC에서 요청 마다 Thread가 생성되어 Controller를 통해 요청을 수행할텐데, 어떻게 1개의 Controller만 생성될 수 있을까요?

Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. 

Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?

Spring Application을 구동할 때 메서드를 실행시키는 방법에 대해 설명해주세요.

의존성과 설정값을 생성자 인자로 주입해야 하는 이유에 대해 설명해주세요.

### JPA

JPA 영속성 컨텍스트의 이점(5가지)을 설명해주세요.JPA Propagation 전파단계를 설명해주세요.JPA를 쓴다면 그 이유에 대해서 설명해주세요.N + 1 문제가 발생하는 이유와 이를 해결하는 방법을 설명해주세요.

### [](https://github.com/ksundong/backend-interview-question#python)Python

GIL에 대해 설명해주세요.Magic method에 대해 설명해주세요.

## [](https://github.com/ksundong/backend-interview-question#%EA%B8%B0%ED%83%80)기타

### [](https://github.com/ksundong/backend-interview-question#%ED%8A%B8%EB%9F%AC%EB%B8%94-%EC%8A%88%ED%8C%85)트러블 슈팅

대용량 트래픽에서 장애가 발생하면 어떻게 대응할 것인가요?

### [](https://github.com/ksundong/backend-interview-question#%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4)디자인 패턴

싱글톤 패턴에 대해서 설명해주세요.(생각보다 어려움)가교 패턴(브릿지 패턴)에 대해서 설명해주세요.전략 패턴에 대해서 설명해주세요.빌더 패턴에 대해서 설명해주세요.팩토리 메서드 패턴에 대해서 설명해주세요.퍼사드 패턴에 대한 예를 들어주세요.

### [](https://github.com/ksundong/backend-interview-question#%ED%85%8C%EC%8A%A4%ED%8A%B8)테스트

테스트 코드에 대해서 어떻게 생각하고, 작성하나요?TDD를 알고 있나요? TDD에 대해서 어떻게 생각하나요?테스트 커버리지에 대해서 어떻게 생각하나요?

### [](https://github.com/ksundong/backend-interview-question#%EC%9D%B8%ED%94%84%EB%9D%BC%ED%81%B4%EB%9D%BC%EC%9A%B0%EB%93%9C)인프라/클라우드

AWS 인프라를 구축해보았다면 설명해주세요.로드 밸런서에 대해서 설명해주세요.리버스 프록시에 대해서 설명해주세요.Fault-tolerant(무정지) 시스템으로 가기 위해 필요한 방법에 대한 생각을 말해주세요.

### [](https://github.com/ksundong/backend-interview-question#%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88)컨테이너

제가 아직 도커, 쿠버네티스에 익숙하지 않아 공부가 좀 더 필요합니다.  
관련해서 질문을 받아본적은 없으나, 일반적인 질문을 담아보았습니다.

Docker란 무엇이고 컨테이너 가상화를 왜 사용할까요?컨테이너 환경에서의 디버깅은 어떤식으로 하며 상대적으로 어려운 점은 무엇인가요?

### [](https://github.com/ksundong/backend-interview-question#devops)DevOps

DevOps는 어쩌면 신입에겐 물어보지 않을 수도 있습니다. 하지만 DevOps가 무엇인지 정도는 알아두는게 좋을 것 같습니다.

CI/CD가 무엇인가요? 왜 CI/CD가 장점이 될까요?DevOps가 무엇인지 설명해주세요.

### [](https://github.com/ksundong/backend-interview-question#%EC%BB%A4%EB%AE%A4%EB%8B%88%EC%BC%80%EC%9D%B4%EC%85%98)커뮤니케이션

정답이 없는 질문입니다. 면접관마다 의도하는 답이 다 다를테니 자신만의 방법을 한 번 쯤 생각해보고 답변에 막힘이 없도록 준비합시다.

어떤 기술이나 방법론이 좋아보일 때, 이를 어떻게 설득할 것인가요?일정이 예상보다 지연될 것 같습니다. 어떻게 해결하실 것인가요?팀원과의 갈등이 있었나요? 있었다면 어떻게 대처했나요?

### [](https://github.com/ksundong/backend-interview-question#%EA%B0%9C%EC%9D%B8%EC%9D%98-%EC%97%AD%EB%9F%89)개인의 역량

본인이 수행한 프로젝트 중 상용화 가능한 프로젝트가 있나요?기술을 습득할 때 어떤 식으로 습득하나요?

### [](https://github.com/ksundong/backend-interview-question#%EC%B5%9C%EC%8B%A0%EA%B8%B0%EC%88%A0%EC%97%90-%EA%B4%80%EC%8B%AC%EC%9D%B4-%EC%9E%88%EB%8A%94%EC%A7%80)최신기술에 관심이 있는지

최신기술에 관심이 있는지 정도를 확인하고자 함입니다. 너무 정확하게 말하지 않아도 관심이 있다는 인상정도를 줄 수 있다면 좋겠습니다.  
그 회사의 기술 스택을 찾아보고 관심을 가져봤다 정도의 느낌을 줄 수 있어야합니다.  
사용까지 해보면 더더욱 좋을 것 같습니다.

protobuf에 대해서 알고계신가요? 이것은 왜 사용할까요?gRPC는 무엇이며, RPC는 무엇인가요? 왜 쓸까요?쿠버네티스가 무엇인가요? 왜 쿠버네티스를 쓸까요?

### [](https://github.com/ksundong/backend-interview-question#%EC%9B%B9%EC%84%9C%EB%B2%84%EC%9D%98-%EB%8F%99%EC%9E%91%EA%B3%BC%EC%A0%95)웹서버의 동작과정

## [](https://github.com/ksundong/backend-interview-question#%EB%A9%B4%EC%A0%91-%EA%BF%80%ED%8C%81)면접 꿀팁

회사의 기술스택에 관심을 가져보세요. 학습능력이 좋음을 어떤식으로 보여줄 수 있을까요?

본인이 수행한 프로젝트를 유의미한 트래픽이 나올정도로 해본 경험을 높게 평가하는 회사가 많습니다.

두괄식으로 답변하도록 합시다. (사실 힘듭니다. 그렇게 될 수 있게끔 연습 또 연습!)

프로젝트를 수행할 때, 내가 이 기술을 단순히 좋아보여서 사용한 것이 아니라, 많은 고민을 했음을 보여주도록 하세요. 가장 간단한 질문으로는 '왜 그 기술을 사용했나요?', '그 기술 말고 다른 기술은 왜 사용하지 않았나요?', '대체할만한 기술이 있나요?' 등이 있습니다.
<!--stackedit_data:
eyJoaXN0b3J5IjpbODU1MzEyNzk0XX0=
-->