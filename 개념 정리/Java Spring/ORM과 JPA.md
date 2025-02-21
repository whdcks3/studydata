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
