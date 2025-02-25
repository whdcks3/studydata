## ORM의 개념
### 객체와 관계형 데이터베이스의 차이점
소프트웨어 개발에서는 데이터를 저장하고 관리하는 방법으로 객체(Object) 기반의 프로그래밍과 관계형 데이터베이스(Relational Database, RDB)를 사용한다. 그러나 이 두 방식은 근본적으로 다르기 때문에, 이를 효과적으로 연결하는 기술이 필요하다.

**객체 지향 프로그래밍(OOP)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터를 클래스와 객체로 표현한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터 간의 관계를 참조(Reference)를 통해 나타낸다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;실행 시점에서 동적으로 데이터가 생성되고, 메모리에서 관리된다.

**관계형 데이터베이스(RDB)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터를 테이블, 행(Row), 열(Column)로 저장한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터 간의 관계는 외래 키(Foreign Key)를 통해 정의된다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;정적인 데이터 저장 방식으로, SQL을 이용해 데이터를 조직한다.

이러한 차이점으로 인해, 객체 모델과 관계형 모델을 그대로 연결하면 여러가지 문제가 발생한다. 예를 들어, 객체 지향 프로그래밍에서는 상속(Inheritance)와 다형성(Polymorphism)을 활용할 수 있지만, 관계형 데이터베이스에서는
이를 직접적으로 지원하지 않는다. 이러한 불일치를 해결하기 위해 ORM(Object-Relational Mapping)이 등장하게 되었다.

-----------
## ORM
ORM(Object-Relational Mapping, 객체-관계 매핑)은 **객체지향 프로그래밍에서 사용하는 객체와 관계형 데이터베이스의 테이블을 자동으로 연결해주는 기술**이다.<br>
개발자는 SQL을 직접 작성하지 않고도 객체 중심의 코드만으로 데이터베이스를 조작할 수 있다.

ORM을 사용하면 다음과 같이 객체와 데이터베이스 테이블 간의 매핑이 이루어진다.
|객체 지향 프로그래밍|관계형 데이터베이스|
|:---|:---|
|클래스(class)|테이블(Table)|
|객체(Object)|행(Row)|
|필드(Field)|열(Column)|
|메서드(Method)|저장 프로시저|

즉, ORM은 객체의 데이터를 데이터베이스에 저장하거나 불러올 때, 개발자가 SQL을 직접 작성하지 않차도 되도록 해준다.

------------
## ORM이 작동하는 방식
**객체를 테이블에 매핑**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ORM은 클래스의 구조를 분석하여 데이터베이스의 테이블과 매핑한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, User라는 클래스가 있다면 ORM은 이를 users라는 테이블에 대응시킨다.

**객체의 필드를 컬럼에 매핑**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클래스의 속성(필드)은 데이터베이스 테이블의 컬럼과 자동으로 매핑된다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어 User클래스의 name 필드는 users테이블의 name 컬럼에 저장된다.

**객체를 저장하면 SQL를 자동으로 생성**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;개발자 User객체를 저장하면, ORM은 자동으로 INSERT SQL를 생성하여 실행된다.

**객체를 조회하면 SQL를 자동으로 실행**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```findById(1)```같은 메서드를 실행하면, ORM은 ```SELECT * FROM users WHERE id=1```같은 SQL을  실행하여 객체를 반환한다.

## ORM을 사용한 예제
Java의 ORM 기술인 JPA(Java Persistence API)를 활용하여 ORM을 사용하는 예제이다.
```java
import jakarta.persistence.*;

@Entity
@Table(name = "users") // users 테이블과 매핑
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY) // 자동 증가 ID
    private Long id;

    @Column(nullable = false)
    private String name;

    // 기본 생성자 필수 (JPA에서 사용)
    public User() {}

    public User(String name) {
        this.name = name;
    }

    public Long getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```
위의 코드에서 ```@Entity``` 애노테이션은 이 클래스가 데이터베이스 테이블과 매핑되는 엔티티임을 의미한다.<br>
ORM이 자동으로 이 클래스를 기반으로 users라는 테이블을 생성하고, 필드들을 컬럼으로 매핑한다.

이제, User객체를 데이터베이스에 저장할 때 SQL을 직접 작성하지 않고도 다음과 같이 수행할 수 있다.
```java
EntityManagerFactory emf = Persistence.createEntityManagerFactory("my-persistence-unit");
EntityManager em = emf.createEntityManager();

em.getTransaction().begin(); // 트랜잭션 시작
User user = new User("홍길동");
em.persist(user); // ORM이 자동으로 INSERT 실행
em.getTransaction().commit(); // 트랜잭션 커밋

em.close();
emf.close();
```
위 코드에서 em.persist(user);를 실행하면 ORM이 자동으로 INSERT INTO users (name) VALUES ('홍길동'); SQL을 실행하여 데이터를 저장한다.

-----------------
## ORM의 장점
**개발 생산성 향상**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SQL을 직접 작성하지 않아도 되므로 개발 속도가 빨라진다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;객체 중심의 프로그래밍이 가능해진다.

**유지보수 용이성**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SQL이 코드 내부에 분산되지 않고, ORM이 이를 관리하기 때문에 유지보수가 쉬워진다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터베이스 변경이 필요할 때, SQL을 직접 수정할 필요 없이 ORM 설정만 변경하면 된다.

**데이터베이스 독립성 보장**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ORM을 사용하면 특정 데이터베이스(MySQL, PostgreSQL, Oracle 등)에 종속되지 않고 쉽게 변경할 수 있다.

**보안 강화**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ORM이 자동으로 SQL을 생성하므로 SQL Injection 같은 보안 취약점이 줄어든다.

## ORM의 단점
**성능 오베허드** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ORM이 SQL을 자동으로 생성하는 과정에서 성능 저하가 발생할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;불필요한 SQL이 실행되거나, 최적화되지 않은 쿼리가 발생할 수 있다.

**복잡한 쿼리 작성 어려움** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ORM은 단순한 CRUD 작업에는 강력하지만 복잡한 조인이나 서브쿼리는 SQL을 직접 작성하는 것이 유리할 때가 있다.

**학습 곡선**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ORM의 개념과 동작 방식을 이해해야 하므로, SQL을 직접 사용하는 것보다 학습 비용이 높을 수 있다.

-----------
## ORM을 사용할 때 고려할 점
**데이터 조회 성능**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 대량 데이터를 조회할 때는 ```Lazy Loading(지연 로딩), ```Fetch join```등의 기법을 활용하여 성능 최적화를 해야 한다.

**트랜잭션 관리**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ORM은 내부적으로 트랜잭션을 관리하기 때문에, 개발자는 이를 잘 이해하고 ```@Transactional```등을 적절히 활용해야 한다.

**필요에 따라 SQL을 직접 사용**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;복잡한 보고서 조회나 다량의 데이터 업데이트가 필요한 경우, ORM보다는 JPQL 또는 Native Query를 활용하는 것이 더 효율적일 수 있다.

--------------------
## 주요 ORM 프레임 워크
객체-관계 매핑(ORM)은 데이터베이스와 객체 지향 프로그래밍 간의 불일치를 해결하기 위한 기술이다. 이를 구현하는 대표적인 프레임워크는 **JPA(Java Persistence API),Hibernate, MyBatis**가 있으며, 각각의 특징과 차이점을 이해하는것이 좋다.

## JPA(Java Persistence API)
JPA(Java Persistence API)는 자바의 공식 ORM 표준 명세로, 객체와 관계형 데이터베이스를 연결하는 공통 API를 제공한다. JPA 자체는 구현체가 아니며, 개발자는 JPA를 지원하는 구현체(ex:Hibernate,EclipseLink,OpenJPA 등)을 선택하여 사용할 수 있다.)

**JPA의 핵심 역할**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;엔티티(Entity)와 데이터베이스 테이블을 매핑한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;객체 기반으로, 데이터 조작을 수행하도록 지원한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;영속성 컨텍스트(Persistence Context)를 관리하여 데이터의 상태를 유지한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;트랜잭션 및 데이터 변경을 자동으로 관리한다.<br>

**JPA의 주요 특징**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;표준 인터페이스 : 특정 벤더(Hibernate,EclipseLinke 등)에 종속되지 않음<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SQL 작성이 불필요 : 객체를 이용한 데이터 조작 가능<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JPQL(Java Persistence Query Language) 제공 : 객체 기반의 쿼리 작성<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;캐싱과 최적화 기능 제공

```java
import jakarta.persistence.*;

@Entity
@Table(name = "users")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String name;

    protected User() {}

    public User(String name) {
        this.name = name;
    }

    public Long getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```
위 코드는 User 클래스를 users테이블과 매핑하는 JPA 엔티티이다. @Entity는 이 클래스가 JPA 엔티티임을 명시한다.<br>
JPA 단독으로 사용하기보다는 구현체화 함께 사용해야 하며, 대표적인 구현체 중 하나가 Hibernate이다.

-------------
### Hibernate
Hibernate는 JPA의 가장 널리 사용되는 구현체로, 객체와 관계형 데이터베이스를 매핑하는 강력한 기능을 제공한다. JPA 명세를 따르면서도, JPA에서 지원하지 않는 다양한 고급 기능(캐싱, 배치 처리, 지연 로딩 최적화 등)을 포함하고 있다.

**Hibernate의 주요 특징**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JPA의 구현체로, JPA API를 사용할 수 있음<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터베이스 독립성을 보장하며, 다양한 데이터베이스를 지원<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1차 캐시 및 2차 캐시를 활용하여 성능 최적화 가능<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;고급 쿼리 기능(HQL, Criteria API) 제공

Hibernate를 사용하면 SQL을 직접 작성하지 않고도 객체 중심으로 데이터 조작이 가능하다.<br>
예를 들어, User 엔티티를 Hibernate로 저장하는 코드는 다음과 같다
```java
EntityManagerFactory emf = Persistence.createEntityManagerFactory("my-persistence-unit");
EntityManager em = emf.createEntityManager();

em.getTransaction().begin();
User user = new User("김철수");
em.persist(user);
em.getTransaction().commit();

em.close();
emf.close();
```
위 코드에서 persist(user)를 호출하면 Hibernate가 자동으로 INSERT INTO users (name) VALUES ('김철수') SQL을 실행한다.<br>
Hiberante는 JPA의 기능을 확장하여 제공하므로, JPA를 사용할 때 기본적으로 Hibernate를 함께 활용하는 경우가 많다.

--------------
### MyBatis
MyBatis는 JPA 및 Hibernate와는 다르게 SQL 기반의 반(半)ORM 프레임워크다. 즉, 객체와 데이터베이스 간의 매핑을 지원하지만, SQL을 직접 작성하는 방식을 따른다.

**MyBatis의 주요 특징**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SQL을 직접 작성하여 데이터베이스를 제어할 수 있음<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;객체 매핑을 지원하지만, SQL 자동 생성 기능은 없음<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JPA나 Hiberante보다 더 정밀한 SQL 제어가 가능<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;복잡한 쿼리를 작성해야 하는 경우 적합

MyBatis는 XML 기반으로 SQL을 정의하고, Java 코드에서 이를 호출하는 방식으로 동작한다.<br>
예를 들어, User 데이터를 조회하는 MyBatis XML 매핑 파일(UserMapper.xml)은 다음과 같다.
```java
<mapper namespace="com.example.mapper.UserMapper">
    <select id="findById" parameterType="long" resultType="com.example.model.User">
        SELECT * FROM users WHERE id = #{id}
    </select>
</mapper>
```
그리고 이를 Java 코드에서 호출할 때는 다음과 같이 사용한다.
```java
public interface UserMapper {
    User findById(@Param("id") Long id);
}
```
MyBastis는 SQL를 직접 관리하기 때문에, 복잡한 SQL이 필요한 경우에는 유용하지만, 객체 중심의 프로그래밍과는 거리가 있다.

### ORM 프레임워크 비교
|특징|JPA|Hibernate|MyBatis|
|:---|:---|:---|:---|
|SQL 자동 생성|O|O|X|
|데이터베이스 독립성|O|O|X|
|객체 매핑|O|O|X|
|SQL 직접제어|X|X|O|
|캐싱 기능|O|O(확장 기능 포함)|X|
|학습 난이도|높음|높음|중간|
|복잡한 쿼리 작성|어려움|어려움|쉬움|

JPA는 표준 ORM API이며, 특정 구현체(Hibernate, EclipseLink 등)을 사용해야 한다.<br>
Hibernate는 JPA의 구현체로, JPA보다 확장된 기능을 제공한다.<br>
MyBatis는 SQL을 직접 작성해야 하지만, 세밀한 쿼리 제어가 가능하다.

-------------
#### 어떤 ORM을 선택해야 할까?
**JPA + Hibernate 조합**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;객체 중심의 프로그래밍을 선호한다면 JPA + Hibernate 조합이 적합하다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SQL을 직접 작성할 필요 없이, 비즈니스 로직에 집중할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;그러나 복잡한 쿼리를 다룰 때는 최적화가 필요하다.

**MyBatis**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터베이스에 대한 제어권이 중요하다면 MyBatis가 적합하다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;복잡한 SQL을 직접 작성해야 하지만, 성능 최적화와 세밀한 데이터 처리가 가능하다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;그러나 객체 중심의 개발보다는 SQL 중심의 개발이 필요하다.

-----------------------
## JPA의 개념
JPA(Java Persistence API)는 자바 애플리케이션에서 **객체와 관계형 데이터베이스(RDBMS)** 간의 데이터를 쉽게 매핑하고 조작할 수 있도록 설계된 ORM 표준 명세이다.<br>
기존의 JDBC를 직접 활용하여 SQL을 작성하고 데이터를 조작하는 방식과 달리, JPA는 **객체 중심의 프로그래밍 방식**을 유지하면서도 데이터 저장소와의 매핑을 효율적으로 수행한다.

JPA는 Java EE(Enterprise Edition)의 일부로 등장하였으며, 현재는 **Jakarta EE**의 일부로 포함되어 있다.<br>
하지만 JPA자체는 구현체가 아닌 API이므로, 실제로 API를 사용하려면 Hibernate, EclipseLink, OpenJPA 등의 구현체를 사용해야 한다.

--------------
## JPA의 핵심 개념
**엔티티(Entity) 매핑** : 자바 클래스와 데이터베이스 테이블을 매핑하는 방식<br>
**영속성 컨텍스트(Persistence Context)** : 엔티티 객체의 생명주기를 관리하는 개념<br>
**JPQL(Java Persistence Query Language)** : SQL과 유사하지만 객체를 대상으로 하는 쿼리 언어<br>
**트랜잭션 관리** : 데이터 변경 사항을 안전하게 처리하는 기능<br>

--------------------
## JPA의 주요 기능
JPA는 객체와 관계형 데이터베이스 간의 매핑을 자동화하고, 데이터 조작을 효율적으로 수행할 수 있도록 다음과 같은 기능을 제공한다.

**엔티티(Entity)와 테이블 매핑**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```@Entity```애노테이션을 사용하여 자바 클래스를 데이터과 연결할 수 잇다.

**데이터 저장(Persist)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```EntityManager.persist()```를 이용해 객체를 데이터베이스에 저장한다.

**데이터 조회(Find)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```EntityManager.find()```를 이용해 데이터베이스에석 객체를 조회한다.

**데이터 수정(Update)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JPA는 변경 감지(Dirty Checking)기능을 통해 ```persist()```없이도 자동으로 변경 사항을 반영한다.

**데이터 삭제(Delete)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```EntityManager.remove()```를 호출하여 데이터를 삭제할 수 있다.

**JPQL(Java Persistence Query Language)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;객체를 대상으로 하는 쿼리를 작성하여 데이터베이스에서 원하는 정보를 조회할 수 있다.

------------
### JPA를 이용한 기본적인 데이터 저장 예제
```java
import jakarta.persistence.*;

@Entity
@Table(name = "users")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String name;

    protected User() {}

    public User(String name) {
        this.name = name;
    }

    public Long getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

```EntityManager```를 사용해서 저장하는 것도 보자
```java
EntityManagerFactory emf = Persistence.createEntityManagerFactory("my-persistence-unit");
EntityManager em = emf.createEntityManager();

em.getTransaction().begin(); // 트랜잭션 시작
User user = new User("김철수");
em.persist(user); // 데이터 저장
em.getTransaction().commit(); // 트랜잭션 커밋

em.close();
emf.close();
```
--------------
### JPA의 장점
+ SQL을 직접 작성하지 않아도 되므로 생산성이 향상된다.
+ 데이터베이스 변경 시 애플리케이션 코드의 수정이 최소화된다.
+ 트랜잭션과 변경 감지를 자동으로 처리하여 데이터 일관성 유지가 용이하다.
+ 객체 중심의 개발이 가능하므로 비즈니스 로직에 집중할 수 있다.

### JPA의 단점
+ SQL에 익숙한 개발자에게는 학습 곡선이 높을 수 있다.
+ 복잡한 쿼리를 작성할 때는 JPQL이 SQL보다 어려울 수 있다.
+ 대규모 트랜잭션에서는 성능 최적화를 고려해야 한다.
+ 데이터베이스에 따라 최적화가 필요할 수 있다.

--------------
## JPA와 Hibernate의 관계
JPA는 객체와 관계형 데이터베이스(RDBMS)를 연결하는 Java의 표준 API며, Hibernate는 JPA의 대표적인 구현체(Implementation)이다.<br>
JPA 자체는 데이터베이스와 직접 연결되지 않으며, 이를 사용하려면 반드시 구현체가 필요하다. Hibernate는 JPA의 구현체 중 가장 널리 사용되는 프레임워크로, JPA가 제공하는 인터페이스를 실제로 동작하도록 구현한다.

### JPA와 Hibernate의 역할 구분
**JPA(Java Persistence API)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;자바 애플리케이션에서 ORM을 표준화한 인터페이스 및 명세이다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;특정 구현체에 의존하지 않고 **객체와 관계형 데이터베이스를 매핑하는 기능**을 정의한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```javax.persistence``` 혹은 ```jakarta.persistence```패키지 내 인터페이스를 제공한다.

**Hibernate**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JPA의 대표적인 구현체로서, **JPA가 제공하는 표준 인터페이스를 실제로 구현**한 프레임워크이다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;단순한 JPA 구현체를 넘어, **JPA 표준 외에도 추가적인 성능 최적화 및 확장 기능**을 제공한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```org.hibernate```패키지를 사용하여, JPA 명세를 기반으로 동작한다.

즉, JPA는 규칙(Interface), Hibernate는 실제 구현(Implementation) 이라고 이해하면 된다.

### JPA와 Hibernate의 관계 정리
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; JPA는 ORM을 위한 표준 명세이고, Hibernate는 이를 구현한 프레임워크이다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JPA는 EntityManager를 사용하여 데이터 저장, 조회, 삭제 등의 기능을 제공한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hibernate는 EntityManager 내부에서 JPA가 정의한 메서드를 실제로 구현하고 SQL을 실행한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JPA를 사용하면 특정 구현체(Hibernate, EclipseLink 등)에 의존하지 않는 개발이 가능하지만, 대부분의 경우 Hibernate가 가장 널리 사용된다.

------------------
## JPA의 주요 기능
JPA는 Java 애플리케이션에서 객체를 관계형 데이터베이스에 저정하고 관리하는 데 필요한 다양한 기능을 제공한다. JPA가 제공하는 핵심기능들은 엔티티 매핑, 영속성 컨텍스트, 트랜잭션 처리, JPQL(Java Persistence Query Lanugage)등으로 나눌 수 있다.

JPA를 활용하면 개발자는 직접 SQL을 사용하지 않고도 객체를 데이터베이스에 저장, 조회, 수정, 삭제할 수 있으며, 트랜잭션을 통해 데이터의 일관성을 보장할 수 있다.

-------------
### 엔티티(Entity) 매핑
JPA의 가장 기본적인 기능은 객체와 데이터베이스 테이블을 매핑(Mapping)하는 기능이다. 엔티티(Entity)는 JPA에서 데이터베이스 테이블과 매핑되는 자바 객체를 의미한다.<br>
-> 엔티티를 선언하기 위해 ```@Entity```애노테이션을 사용하며, 이를 통해 JPA가 해당 클래스를 데이터베이스를 연결할 수 있도록 한다.
-> 테이블 이름을 명시적으로 지정하려면 ```@Table(name = "테이블명")``` 애노테이션을 추가할 수 있다.

예제
```java
import jakarta.persistence.*;

@Entity
@Table(name = "users")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String name;

    protected User() {}

    public User(String name) {
        this.name = name;
    }

    // Getter 및 Setter
}
```
----------
### 영속성 컨텍스트(Persistence Context)
JPA에서 가장 중요한 개념 중 하나가 영속성 컨텍스트(Persistence Context)이다.<br>
영속성 컨텍스트는 **엔티티 객체의 상태를 관리하는 공간**으로, 엔티티 객체가 생성되거나 조회될 때 이를 캐싱하여 데이터베이스와의 불필요한 상호작용을 줄인다.
-> JPA에서 데이터를 조회하면, 동일한 트랜잭션 내에서는 같은 엔티티 객체를 재사용할 수 있다.
-> 데이터 변경이 발생하면, JPA는 이를 자동으로 감지(Dirty Checking)하여 변경된 데이터만 반영한다.

예제
```java
EntityManagerFactory emf = Persistence.createEntityManagerFactory("my-persistence-unit");
EntityManager em = emf.createEntityManager();

em.getTransaction().begin();
User user1 = em.find(User.class, 1L);  // 데이터 조회
User user2 = em.find(User.class, 1L);  // 같은 트랜잭션 내에서 동일한 객체 반환
em.getTransaction().commit();

em.close();
emf.close();
```
-------------------
### 트랜잭션(Transaction) 관리
JPA는 트랜잭션을 기반으로 데이터의 일관성을 유지한다.<br>
트랜잭션을 사용하면 여러 개의 데이터 조작 작업을 하나의 논리적인 작업 단위로 묶어서 실행할 수 있으며, 이를 통해 데이터 정합성을 보장할 수 있다.

JPA의 트랜잭션은 ```EntityManager.getTransaction().begin()```을 통해 명시적으로 시작되며, ```commit()```를 호출해야 변경 사항이 반영된다.

예제
```java
EntityManagerFactory emf = Persistence.createEntityManagerFactory("my-persistence-unit");
EntityManager em = emf.createEntityManager();

em.getTransaction().begin();  // 트랜잭션 시작
User user = new User("홍길동");
em.persist(user);  // 엔티티 저장
em.getTransaction().commit();  // 트랜잭션 커밋

em.close();
emf.close();
```
```persist(user)```를 호출했을 때 바로 데이터베이스에 INSERT 쿼리가 실행되지 않는다.
트랜잭션이 ```commit()```되었을 때 JPA가 변경 내용을 감지하고 실제로 데이터베이스에 반영한다.

-----------------
### JPQL(Java Persistence Query Language)
JPA는 SQL과 유사한 JPQL을 제공한다.<br>
JPQL은 객체(Entity)를 대상으로 하는 쿼리 언어로, SQL과 달리 테이블이 아니라 엔티티 객체를 대상으로 동작한다.

예제
```java
TypedQuery<User> query = em.createQuery("SELECT u FROM User u WHERE u.name = :name", User.class);
query.setParameter("name", "홍길동");
List<User> users = query.getResultList();
```
코드에서 "SELECT u FROM User u WHERE u.name = :name" 쿼리는 users 테이블이 아니라 User 엔티티를 대상으로 동작한다.

 ---------------------------
 ## 엔티티와 테이블 매핑
 JPA를 사용하기 위해서는 엔티티 개념을 정확히 이해하고 이를 데이터베이스 테이블과 매핑하는 과정이 필수적이다.<br>
JPA는 엔티티를 이용하여 객체와 테이블을 연결하며, 이를 통해 객체지향적인 방식으로 데이터를 다룰 수 있도록 지원한다.

### 엔티티(Entity)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;엔티티(Entity)란 데이터베이스의 테이블과 매핑되는 객체를 의미한다.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JPA에서는 엔티티를 정의할 때 @Entity 애노테이션을 사용해야 한다.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;객체지향 프로그래밍 방식을 유지하면서도 데이터베이스의 테이블과 쉽게 연동할 수 있도록 도와준다.
```java
import jakarta.persistence.*;

@Entity  // 이 클래스를 엔티티로 선언
@Table(name = "users")  // 매핑할 테이블 지정
public class User {

    @Id  // 기본 키(PK) 지정
    @GeneratedValue(strategy = GenerationType.IDENTITY)  // 자동 증가 전략
    private Long id;

    @Column(nullable = false, length = 100)  // name 필드를 테이블의 name 컬럼과 매핑
    private String name;

    protected User() {}

    public User(String name) {
        this.name = name;
    }

    // Getter 및 Setter 생략
}
```
------------------
### @Entity 애노테이션
```@Entity```애노테이션은 JPA가 해당 클래스를 엔티티로 인식할 수 있도록 설정하는 필수적인 애노테이션이다.
-> @Entity가 선언된 클래스는 **반드시 기본 생성자가 있어야 한다**(protected 또는 public 생성자)
-> @Entity가 선언된 클래스는 반드시 기본 키(@Id)를 가져야 한다.
```java
@Entity
public class Product {
    @Id
    private Long id;
}
```
만약 @Entity를 선언한 클래스에 기본 키를 지정하지 않으면, JPA 실행 시 오류가 발생한다.

--------------
### @Table 애노테이션
기본적으로 엔티티의 클래스명은 데이터베이스 테이블명과 자동으로 매핑된다.<br>
하지만 테이블명이 다를 경우 ```@Table(name = "테이블명")``` 애노테이션을 사용하여 지정할 수 있다.
```java
@Entity
@Table(name = "products")
public class Product {
    @Id
    private Long id;
}
```
위 코드는 Product 클래스가 products라는 테이블과 매핑되도록 설정한 것이다.
만약 @Table 애노테이션을 사용하지 않으면, JPA는 클래스 이름을 그대로 테이블명으로 사용한다.

---------------
### @Id와 기본 키 매핑
모든 엔티티 클래스는 반드시 기본 키(Primary Key)를 가져야 하며, JPA는 기본 키를 기준으로 엔티티 객체를 관리한다.<br>
기본 키는 @Id 애노테이션을 통해 지정할 수 있으며, 기본 키 값을 자동으로 생성할 수도 있다.

기본 키를 자동으로 생성하는 방법은 다음과 같이 ```@GeneratedValue```를 활용할 수 있다.
```java
@Entity
public class Order {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String orderNumber;
}
```
```GenerationType.IDENTITY``` : 데이터베이스가 자동으로 기본 키를 생성하도록 설정한다.(예: MySQL의 AUTO_INCREMENT)<br>
```GenerationType.SEQUENCE``` : 데이터베이스의 시퀀스를 활용하여 기본 키를 생성한다. (주로 PostgreSQL, Oracle에서 사용)<br>
```GenerationType.TABLE``` : 키 생성 전용 테이블을 사용하여 기본 키를 관리한다.<br>
```GenerationType.AUTO``` : 데이터베이스 방언에 맞게 자동으로 선택된다.

-----------------
### @Column 애노테이션
@Column 애노테이션은 엔티티의 필드를 데이터베이스의 컬럼과 매핑할 때 사용한다.<br>
생략하면 필드 이름이 자동으로 컬럼명이 되지만, 필요한 경우 명시적으로 설정할 수도 있다.
```java
@Entity
public class Customer {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "customer_name", nullable = false, length = 50)
    private String name;
}
```
위 코드에서 name 필드는 customer_name이라는 컬럼과 매핑되며,<br>
```nullable = false``` : 해당 컬럼이 NULL 값을 허용하지 않도록 설정한다.<br>
```length = 50``` : 문자열 길이를 최대 50자로 제한한다.

-------------
### @Transient 애노테이션
JPA는 엔티티 객체의 모든 필드가 자동으로 컬럼으로 매핑되지만,<br>
**일부 필드는 데이터베이스와 매핑하지 않고, 객체 내부에서만 사용하고 싶은 경우**가 있다.<br>
이때 ```@Transient``` 애노테이션을 사용하면 해당 필드는 데이터베이스와 무관한 필드로 취급된다.
```java
@Entity
public class Product {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @Transient
    private int discountPrice;  // 데이터베이스 컬럼으로 매핑되지 않음
}
```
discountPrice 필드는 데이터베이스에 저장되지 않고, 애플리케이션 내부에서만 사용된다.
계산된 값을 임시적으로 저장하거나, 특정 로직에서만 필요한 데이터를 관리할 때 활용된다.

-----------
## 필드 매핑
JPA에서는 엔티티의 각 필드가 데이터베이스의 컬럼과 자동으로 매핑된다. 하지만 단순히 필드명과 컬럼명을 일치시키는 것만으로는 충분하지 않다.
데이터베이스 스키마 설계에 따라 필드의 속성을 세밀하게 조정해야 하는 경우가 많으며, 이를 위해 JPA는 다양한 매핑 애노테이션을 제공한다.

### 기본적인 필드 매핑
JPA에서는 **엔티티의 필드명을 기반으로 자동으로 데이터베이스의 컬럼을 생성**한다.<br>
예를 들어, name필드가 있다면, 이를 자동으로 name이라는 컬럼으로 매핑한다.
```java
@Entity
public class Member {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;  // 자동으로 'name' 컬럼에 매핑됨

    private int age;  // 자동으로 'age' 컬럼에 매핑됨
}
```
이처럼 필드 이름과 컬럼 이름이 같다면 별도의 설정 없이 자동으로 매핑된다.<br>
하지만 컬럼명을 직접 지정하거나 추가적인 설정이 필요한 경우 @Column 애노테이션을 활용할 수 있다.

--------------------
### @Column 애노테이션
```@Column``` 애노테이션을 사용하면 컬럼의 이름, 길이, 제약 조건 등을 직접 설정할 수 있다.
```java
@Entity
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "emp_name", length = 100, nullable = false, unique = true)
    private String name;

    @Column(name = "salary", precision = 10, scale = 2)
    private Double salary;
}
```
위 코드를 보면 @Column 애노테이션을 통해 컬럼의 속성을 설정할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```name``` : 컬럼명을 명시적으로 지정 (기본값은 필드명과 동일)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```length``` : 문자열의 최대 길이 지정 (기본값 : 255)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```nullable``` : false로 설정하면 Not Null 제약 조건이 추가됨<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```unique``` : true로 설정하면 해당 컬럼에 UNIQUE 제약 조건이 추가됨<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```precision``` 및 ```scale``` : BigDecimal 또는 Double과 같은 숫자형 데이터의 정밀도와 소수점 자리수를 설정

**주의할 점**<br>
```nullable = false```로 설정하면, 데이터가 반드시 존재해야 하므로, 데이터 입력시 null값을 허용하지 않는다.<br>
```unique = true```는 데이터베이스 수준에서 유니크 제약 조건을 추가한다. 하지만 인덱스 생성까지 포함하지는 않으므로 성능 최적화를 위해 추가적인 인덱스 설정이 필요할 수 있다.

----------------
### @Transient 애노테이션
일부 필드는 **데이터베이스에 저장되지 않고 애플리케이션 내에서만 사용될 수 있다.** <br>
이러한 필드는 @Transient 애노테이션을 사용하여 매핑에서 제외할 수 있다.
```java
@Entity
public class Product {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @Transient
    private int discountedPrice;  // 데이터베이스 컬럼으로 매핑되지 않음
}
```
discountedPrice 필드는 데이터베이스에 저장되지 않고, 애플리케이션 내부에서만 사용된다.<br>
예를 들어, 할인가를 계산하여 UI에서 표시해야 하지만, 데이터베이스에 저장할 필요가 없는 경우 유용하게 사용할 수 있다.

----------------
### @Lob 애노테이션
대용량 데이터(Lob, Large Object)를 저장할 때 사용되는 애노테이션이다.<br>
LOB데이터는 텍스트 또는 바이너리(BLOB)형태로 저장될 수 있다.
```java
@Entity
public class Article {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Lob
    @Column(columnDefinition = "TEXT")  // MySQL에서는 columnDefinition 필요
    private String content;  // 긴 문자열 저장

    @Lob
    private byte[] image;  // 이미지 파일 등 바이너리 데이터 저장
}
```
```@Lo```b을 사용하면 데이터베이스의 TEXT 또는 BLOB 타입으로 매핑된다.<br>
```String``` 타입에 사용하면 ```CLOB(Character Large Object)```,<br>
```byte[]``` 타입에 사용하면 ```BLOB(Binary Large Object)```으로 매핑된다.

**주의할 점**<br>
@Lob 필드는 데이터 크기가 크기 때문에 조회 및 수정 성능 저하 가능성이 있다.<br>
MySQL에서는 TEXT 또는 BLOB을 명확하게 지정해야 오류가 발생하지 않는다.

----------------
### @Enumerated 애노테이션
Java의 enum 타입을 데이터베이스에 저장하려면 ```@Enmberated``` 애노테이션을 사용해야 한다.<br>
기본적으로 enum타입은 ORDINAL(숫자) 또는 STRING(문자열) 방식으로 저장할 수 있다.
```java
public enum Role {
    USER, ADMIN, MANAGER
}

@Entity
public class Account {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Enumerated(EnumType.STRING)  // ENUM 값을 문자열로 저장
    private Role role;
}
```
```EnumType.ORDINAL```(기본값) : ```USER(0), ADMIN(1), MANAGER(2)``` 처럼 숫자로 저장됨<br>
-> 순서 변경 시 데이터 문제 발생 가능하므로 권장되지 않음<br>
```EnumType.STRING``` : ```USER, ADMIN, MANAGER``` 처럼 문자열 그대로 저장됨<br>
-> 값이 변경되어도 안전하며, 유지보수 측면에서 권장됨

**주의할 점**<br>
```EnumType.ORDINAL``` 방식은 ENUM 순서가 변경되면 기존 데이터가 잘못 매핑될 위험이 있다.
```EnumType.STRING``` 방식을 권장하지만, 저장 공간이 더 필요할 수 있다.

-------------
## 관계 매핑
JPA에서는 객체 간의 관계를 데이터베이스 테이블의 관계와 연결하여 관리할 수 있도록 다양한 연관 관계 매핑을 지원한다.<br>
이러한 관계 매핑을 활용하면 데이터베이스의 외래 키(Foreign Key) 개념을 객체 지향적인 방식으로 사용할 수 있다.<br>
객체 간 관계를 매핑할 때는 크게 다음과 같은 네 가지 방식이 존재한다.

+ 일대일(OneToOne)
+ 일대다(OneToMany)
+ 다대일(ManyToOne)
+ 다대다(ManyToMany)

-----------
### 일대일(OneToOne) 관계
일대일 관계는 한 엔티티가 다른 엔티티와 1:1로 연결될 때 사용된다.<br>
예를 들어, ```User``` 엔티티가 ```UserDetail``` 엔티티와 1:1 관계를 가질 수 있다.
```java
@Entity
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String username;

    @OneToOne
    @JoinColumn(name = "user_detail_id")  // 외래 키를 지정
    private UserDetail userDetail;
}
@Entity
public class UserDetail {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String address;
}
```
```@OneToOne``` : 1:1 관계를 설정하는 애노테이션
```@JoinColumn(name = "user_detail_id")``` : 외래 키 컬럼을 직접 지정
위 코드에서는 ```User``` 엔티티가 ```UserDetail``` 엔티티를 참조하는 관계를 맺고 있으며, user_detail_id가 외래 키로 사용된다.

**일대일 관계의 특징**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;하나의 User는 하나의 UserDetail만을 가질 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;하나의 UserDetail은 하나의 User만을 가질 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;외래 키를 어느 테이블에 둘 것인지 결정할 수 있으며, 기본적으로 주 테이블(User)에 배치하는 것이 일반적이다.

--------------
### 일대다(OneToMany) 관계
일대다 관계는 하나의 엔티티가 여러 개의 엔티티를 가질 수 있는 경우 사용된다.<br>
예를 들어, 하나의 Department는 여러 개의 Employee를 가질 수 있다.
```java
@Entity
public class Department {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @OneToMany(mappedBy = "department")
    private List<Employee> employees = new ArrayList<>();
}
@Entity
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;
}
```
```@OneToMany(mappedBy = "department")``` : Department 엔티티가 여러 개의 Employee를 가질 수 있도록 설정<br>
```@ManyToOne``` : Employee가 Department를 참조하도록 설정<br>
```@JoinColumn(name = "department_id")``` : Employee 테이블이 department_id를 외래 키로 가짐

**일대다 관계의 특징**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```OneToMany``` 관계는 mappedBy를 설정하여 외래 키를 다측(Many) 엔티티에 둔다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;다측(Many) 엔티티(Employee)는 반드시 @ManyToOne을 사용하여 외래 키를 직접 관리해야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Department는 여러 Employee를 포함할 수 있지만, 각 Employee는 하나의 Department만 가질 수 있다.

------------------
### 다대일(ManyToOne) 관계
다대일 관계는 여러 개의 엔티티가 하나의 엔티티를 참조하는 경우 사용된다.<br>
이는 앞서 본 일대다(OneToMany) 관계와 반대 방향이다.
```java
@Entity
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;
}
```
위의 Employee 엔티티는 ManyToOne 관계를 통해 Department 엔티티를 참조한다.<br>
이는 여러 명의 직원이 하나의 부서에 속할 수 있지만, 한 직원은 하나의 부서만 가질 수 있는 상황을 나타낸다.

**다대일 관계의 특징**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```@ManyToOne```을 사용하여 다수의 엔티티가 하나의 엔티티를 참조할 수 있도록 설정한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```@JoinColumn(name = "department_id")```를 지정하여 외래 키를 직접 관리한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;다대일 관계는 일대다 관계의 반대 방향이며, 이를 조합하여 양방향 관계를 설정할 수 있다.

------------------
### 다대다(ManyToMany) 관계
다대다 관계는 한 엔티티가 여러 개의 엔티티를 가질 수 있으며, 동시에 다른 엔티티도 여러 개의 관계를 가질 수 있는 경우 사용된다.<br>
예를 들어, Student와 Course는 다대다 관계를 가질 수 있다.<br>
즉, 하나의 학생(Student)은 여러 과목(Course)을 수강할 수 있고, 하나의 과목(Course)도 여러 학생이 들을 수 있다.
```java
@Entity
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @ManyToMany
    @JoinTable(
        name = "student_course",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private List<Course> courses = new ArrayList<>();
}
@Entity
public class Course {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String title;

    @ManyToMany(mappedBy = "courses")
    private List<Student> students = new ArrayList<>();
}
```
```@ManyToMany```는 다대다 관계를 설정하는 애노테이션이다.<br>
```@JoinTable```을 사용하여 중간 테이블(student_course)을 생성하고, 관계를 정의한다.<br>
```joinColumns = @JoinColumn(name = "student_id")``` → Student의 외래 키<br>
```inverseJoinColumns = @JoinColumn(name = "course_id")``` → Course의 외래 키

**다대다 관계의 특징**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;다대다 관계에서는 **중간 테이블을 생성하여 매핑하는 것이 일반적**이다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```@ManyToMany(mappedBy = "courses")```를 사용하여 반대 방향의 관계도 설정할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;다대다 관계는 자주 사용되지 않으며, 중간 엔티티를 따로 만들어 OneToMany + ManyToOne 구조로 바꾸는 것이 더 일반적이다.
