# Jemeter

jMeter 는 오픈 소스 테스팅 소프트웨어이다. 100% 자바로 작성된 부하 성능 테스팅을 위한 어플리케이션이다. jMeter 는 부하 테스팅, 함수 테스팅, 성능 테스팅, regression(퇴행) 테스팅 등의 다양한 테스트들을 할 수 있도록 고안되었다. JDK5 이상에서 동작한다.

test plans, listeners, functions, 그리고 regular expressions 들을 살펴본다.

그 전에 어플리케이션 테스팅과 연관된 전문 용어들을 살펴본다.

Performance Test
: 주어진 인프라 설정에서 가능한 최고의 성능 기대치를 정한다. 어플리케이션이 상용화되기 전에 수정해야하는 게 있다면 테스팅 과정에서 초반에 알려준다.

Load Test
: 기본적으로 시스템이 작동되는 것을 전제로 최대치의 부하에서 시스템을 테스트한다.

Stress Test
: 리소스를 압도하여 시스템을 깨는 테스트이다.

## JMeter 는 무엇인가
JMeter 는 부하 테스트, 성능 기반의 비즈니스(함수형) 테스트, regression 테스트 등을 다른 프로토콜과 기술 위에서 수행할 수 있는 소프트웨어다. 
아파치 소프트웨어 재단의 Stefano Mazzocchi 는 JMeter 원년 개발자이다. 그는 Apache Tomcat project 의 성능을 테스트하기 위해 JMeter 를 만들었다. 이후에 아파치는 JMeter 를  GUI 를 개선하고 함수적인 테스팅도 가능하도록 하기위해서 새로 설계하였다. 

JMeter 는 Swing graphical API 를 사용하는 시각적 인터페이스를 제공하는 자바 데스크탑 어플리케이션이다. 따라서 JVM 을 허용하는 환경과 워크스테이션이면 어디서든 실행할 수 있다. 

JMeter 가 지원하는 프로토콜은 다음과 같다.
-   Web − HTTP, HTTPS sites 'web 1.0' web 2.0 (ajax, flex and flex-ws-amf)
-   Web Services − SOAP / XML-RPC
-   Database via JDBC drivers
-   Directory − LDAP
-   Messaging Oriented service via JMS
-   Service − POP3, IMAP, SMTP
-   FTP Service

JMeter 특성
-   오픈소스 소프트웨어라 무료로 이용 가능
-  간단하고 직관적인 GUI
-  JMeter 는 다양한 서버 타입 (Web - HTTP, HTTPS, SOAP, Database - JDBC, LCAP, JMS, Mail - POP3 등)
- 플랫폼에 독립적인 툴이다. Linux/Unix 에서는 JMeter shell script 를 실행하면되고, Windows 에서는 jmeter.bat 파일을 실행시키면 된다.
- Swing 과 경량의 컴포넌트를 지원한다 (미리 컴파일된 JAR 는 javax.swing.* 패키지들을 사용한다.)
- JMeter 는 test plans 을 XML 형식으로 저장한다. 즉 텍스트 편집기를 사용해서 test plan 을 생성할 수 있다.
- 멀티 스레드 프레임워크는 다수의 스레드에 의한 동시성 샘플링을 가능하게 한다. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg5NzkwMDEyMCwxNzM5MDMyMTIzLDE0MD
k2ODY5OTIsMzE2NDU1NTg1LDkwMzQzNDc5MSwyNjQ4OTU4NSw3
MjUxNDUxMzksLTc0NDQ5NDk4Nl19
-->