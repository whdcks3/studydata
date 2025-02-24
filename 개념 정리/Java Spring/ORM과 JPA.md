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

-------------------
