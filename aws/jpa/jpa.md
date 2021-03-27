# JPA

Java Persistence API 는, 데이터베이스에 엄청난 양의 데이터를 영속적으로 저장하기 위한, 클래스와 메소드들의 모음이다. Persistence (임시 메모리에 데이터베이스 객체의 복사본을 저장) 에 대해 기본적으로 이해하고, JAVA Persistence API (JPA) 를 이해한다.

기업 어플리케이션은, 엄청난 양의 데이터를 저장하고 검색하면서 데이터 연산들을 수행한다. 모든 가능한 저장소 관리 기술들에도 불구하고, 어플리케이션 개발자들은 일반적으로 데이터베이스 연산들을 효율적으로 수행하는데 애쓴다. 

일반적으로 자바 개발자들은 데이터베이스와 상호작용하기 위해서, 많은 코드를 사용하거나 독점적인 프레임워크를 사용한다. 반면 JPA 를 사용하면, 데이터베이스와 상호작업하는 수고가 상당히 줄어든다. JPA 는 자바 프로그램의 객체 모델들과 데이터베이스 프로그램의 관계형 모델들 사이를 이어주는 다리를 만든다. 

관계형 모델과 객체 모델 간의 mismatch
관계형 객체들은 테이블 형식으로 표현된다. 반면 객체 모델들은 객체 형식의 상호 연결된 그래프로 표현된다. 관계형 데이터베이스에서 객체 모델을 저장하고 검색할 때는 아래 이유들 때문에 일부 mismatch 가 발생한다. 

Granularity (세분성) : 객체 모델은 관계형 모델 보다 더 세부적이다.
Subtype : Subtype 은 일부 관계형 데이터베이스에서 지원되지 않는다.  
Identity : 객체 모델과 달리, 동일하게 작성할 때 관계형 모델은 identity 를 나타내지 않는다. 
Associations (연결) : 관계형 모델들은, 객체 도메인 모델을 살펴보는 동안 다수의 관계를 결정할 수 없다.  
Data navigation (데이터 탐색) : 객체 네트워크 내의 객체들 사이의 데이터 탐색은 두 모델이 다르다.

## What is JPA?

Java Persistence API 는 오라클 기업에서 제공하는 데이터베이스에 방대한 양의 데이터를 영속적으로 저장하기 위한 클래스들과 메소드들의 모음이다. 

## Where to use JPA?

관계형 객체 관리를 위해 코드를 작성하는 부담을 줄이기 위해서, 프로그래머들은 'JPA Provider' 프레임워크를 따랐다. 이는 데이터베이스 인스턴스와 쉽게 상호작용하도록 도와주었다. 이후 프레임워크는 JPA 에 잠식되었다.  

![enter image description here](https://www.tutorialspoint.com/jpa/images/jpa_provider.png)

## JPA History

초창기 EJB 버전들은 영속 계층을 비즈니스 로직 계층과 결합된  
Earlier versions of EJB, defined persistence layer combined with business logic layer using javax.ejb.EntityBean Interface.

-   While introducing EJB 3.0, the persistence layer was separated and specified as JPA 1.0 (Java Persistence API). The specifications of this API were released along with the specifications of JAVA EE5 on May 11, 2006 using JSR 220.
    
-   JPA 2.0 was released with the specifications of JAVA EE6 on December 10, 2009 as a part of Java Community Process JSR 317.
    
-   JPA 2.1 was released with the specification of JAVA EE7 on April 22, 2013 using JSR 338.
    

## JPA Providers

JPA is an open source API, therefore various enterprise vendors such as Oracle, Redhat, Eclipse, etc. provide new products by adding the JPA persistence flavor in them. Some of these products include:

**Hibernate, Eclipselink, Toplink, Spring Data JPA, etc.**
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzODEyMzcxMDcsMzY2OTgxMTk5LDE4MD
EzMzUwNjUsNzI4MDExMTU3LDY1MTk1MTQ5LC0xOTUyODU2MzA4
XX0=
-->