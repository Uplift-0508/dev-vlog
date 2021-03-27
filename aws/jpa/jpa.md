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

초창기 EJB 버전들은 영속 계층은 javax.ejb.EntityBean 인터페이스를 사용하여 비즈니스 로직 계층과 결합된  형태로 정의되었다. 

- EJB 3.0 이 소개되는 동안, 영속 계층은 분리되었고, JPA1.0 (Java Persistence API) 로 구체화되었다. 이 API 스펙은 JSR 220 을 사용해서, 2006년 5월 11일 JAVA EE5 스펙과 함께 출시되었다. 

- JPA 2.0 은 2009년 10월 10일 JAVA EE6 스펙과 함께, Java Community Precess JSR 317 의 한 부분으로, 출시되었다. 

- JPA 2.1 은 2013년 4월 22일 JAVA EE7 스펙과 함께 JSR 338을 사용해서 출시되었다. 

## JPA Providers

JPA 는 오픈소스 API 이다. 따라서 Oracle, Redhat, Eclipse 등의 다양한 기업의 회사들이 새로운 제품에 JPA 영속성을 추가해서 제공한다. 이런 제품들에는 Hibernate, Eclipselink, Toplink, Spring Data JPA 등이 있다. 

# Architecture

Java Persistence API 는 비즈니스 엔티티를 관계형 엔티티로 저장하는 source 다. JPA 는 한 엔티티로 PLAIN OLD JAVA OBJECT (POJO) 를 어떻게 정의할지, 그리고 엔티티 간의 관계들을 어떻게 관리할지 보여준다.

## Class Level Architecture

다음 이미지는 JPA 의 클래스 레벨 아키텍처이다. JPA 의 핵심 클래스와 인터페이스를 보여준다.

![enter image description here](https://www.tutorialspoint.com/jpa/images/jpa_class_level_architecture.png)

다음 테이블은 위 아키텍처에서 보여준 각각의 unit 들을 설명한다.

|      Units     | Description                         |
|----------------|-------------------------------------|
| **EntityManagerFactory** | EntityManager 의 팩토리 클래스이다. 다수의 EntityManager 인스턴스를 생성하고 관리한다. |
| **EntityManager** | 인터페이스이다. 객체들의 영속성 연산들을 관리한다. 마치 쿼리 인스턴스를 위한 팩토리 처럼 동작한다. |
| **Entity** | 엔티티들은 영속성 객체들이다. 데이터베이스의 레코드로 저장된다.   |
| **EntityTransaction** | EntityManager 와 1:1 관계를 가진다. 각 EntityManager에 대해, 연산들을 EntityTransaction 클래스가 관리한다.  |
| **Persistence** | 이 클래스는 EntityManagerFactory 인스턴스를 획득하기 위한 static 메소드를 포함한다. |
| **Query** | 이 인터페이스는, 기준에 맞게 관계형 객체들을 획득하기 위해서, 각 JPA 회사들이 구현한다. |

위 클래스들과 인터페이스들은 데이터베이스에 레코드로 엔티티들을 저장하는데 사용한다. 이는 데이터베이스에 데이터를 저장하기 위해 코드를 작성하는 부담을 줄여서 프로그래머들을 돕는다. 이로써 프로그래머들은, 클래스들과 데이터베이스 테이블들을 매핑하는 코드를 작성하는 것 같은 더 중요한 작업에 집중할 수 있다. 

## JPA Class Relationships

위 아키텍처에서 볼 수 있듯이, 클래스들과 인터페이스들 사이의 관계들이 javax.persistence 패키지에 포함되어 있다. 다음 다이어그램은 그들간에 관계를 보여준다.

![enter image description here](https://www.tutorialspoint.com/jpa/images/jpa_class_relationships.png)

- EntityManagerFactory 와 EntityManager 는 1:다 의 관계를 가진다. EntityManagerFactory 는 EntityManager 인스턴스들의 팩토리 클래스이다. 
- 
- EntityManger 와 EntityTransaction 은 1:1 의 관계를 가진다. 각 EntityManager 연산에 대해 한 개의 EntityTransaction 인스턴스가 있다. 

- EntityManager 와 Query 는 1:다 관계를 가진다. 다수의 쿼리는 하나의 EntityManager 인스턴스를 사용해서 실행할 수 있다. 

- EntityManger 와 Entity 는 1:다 관계를 가진다. 하나의 EntityManager 인스턴스는 다수의 Entity 를 관리할 수 있다. 
    
  # ORM Component
  
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNjI0MjE4NCwxNzc1NDE4NTk4LC0yMD
k1NTY3NTc3LDc2NDYxOTI2MiwzNTkxOTUxMjIsMTQzMTUzMjcy
NiwzNjY5ODExOTksMTgwMTMzNTA2NSw3MjgwMTExNTcsNjUxOT
UxNDksLTE5NTI4NTYzMDhdfQ==
-->