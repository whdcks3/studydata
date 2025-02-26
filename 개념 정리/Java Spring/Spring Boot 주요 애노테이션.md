## 애노테이션의 개념
애노테이션(Annotation)은 Java에서 코드에 추가적인 메타데이터를 제공하여 특정 동작을 수행하도록 하는 기능이다.<br>
이는 단순한 주석이 아니라, 컴파일러나 런타임 환경에서 프로그램의 구조와 동작을 정의하는 중요한 역할을 한다.

Spring Boot에서는 애노테이션이 특히 중요한 역할을 한다.
스프링 컨테이너에서 자동으로 빈(Bean) 등록, 의존성 주입(DI), 트랜잭션 관리, AOP(Aspect-Oriented Programming) 등의 기능을 수행하며,
개발자가 복잡한 설정을 단순화하고 보다 직관적으로 코드를 작성할 수 있도록 돕는다.

-------------
## 애노테이션이란?
애노테이션은 클래스, 메서드, 변수, 생성자 등에 추가할 수 있는 특별한 표기법이다.<br>
자바에서 애노테이션은 @ 기호로 시작하며, 해당 애노테이션이 붙은 요소에 대해 특정한 의미를 부여한다.

예를 들어, 다음과 같은 애노테이션이 있다고 하자.
```java
@Override
public void run() {
    System.out.println("Thread is running...");
}
```
여기서 ```@Override```는 해당 메서드가 부모 클래스의 메서드를 재정의하고 있음을 나타내는 애노테이션이다.<br>
컴파일러는 ```@Overrid```e를 통해 올바르게 오버라이드되었는지 검사하며, 잘못된 경우 컴파일 오류를 발생시킨다.

Spring Boot에서는 애노테이션이 더욱 강력한 기능을 수행한다.<br>
예를 들어, 다음과 같은 애노테이션을 사용하면 스프링 애플리케이션의 **서비스 클래스**로 인식할 수 있다.
```java
@Service
public class UserService {
    public String getUser() {
        return "사용자 정보 반환";
    }
}
```
이처럼, 애노테이션은 코드 자체에 추가적인 정보(메타데이터)를 제공하고,
Spring 컨테이너나 런타임 환경에서 이를 활용하여 특정한 동작을 수행하도록 한다.

---------------
## 애노테이션의 주요 특징
애노테이션의 가장 큰 특징은 설정과 구성을 단순화하는 것이다.<br>
과거에는 XML을 사용하여 모든 설정을 수동으로 정의해야 했지만,<br>
애노테이션을 활용하면 XML 없이도 간결하게 애플리케이션을 설정할 수 있다.

다음은 애노테이션의 주요 특징을 정리한 내용이다.

**컴파일러에게 특정 동작을 지시**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Override를 사용하면 부모 클래스의 메서드를 올바르게 오버라이드하는지 검사할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Deprecated를 사용하면 더 이상 사용되지 않는 메서드임을 표시할 수 있다.

**런타임 환경에서 동적으로 활용**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Spring Boot의 @Component, @Service, @Repository 같은 애노테이션은 자동으로 빈을 등록한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Transactional을 사용하면 데이터베이스 트랜잭션을 자동으로 관리할 수 있다.

**프레임워크 및 라이브러리에서 널리 사용됨**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Spring, JPA, Lombok, JUnit 등 다양한 라이브러리에서 애노테이션 기반의 설정을 지원한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, JPA의 @Entity를 사용하면 데이터베이스의 테이블과 매핑할 수 있다.<br>

**메타데이터를 활용하여 코드의 가독성을 높임**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;애노테이션을 사용하면 코드만 보고도 해당 클래스나 메서드가 어떤 역할을 수행하는지 쉽게 이해할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, @RestController가 붙은 클래스는 REST API를 제공하는 컨트롤러라는 것을 직관적으로 알 수 있다.<br>

---------------
### 애노테이션의 기본 유형
애노테이션은 목적과 사용 방법에 따라 여러 가지 유형으로 나뉜다.<br>
크게 컴파일 타임 애노테이션과 런타임 애노테이션으로 구분할 수 있다.

**컴파일 타임 애노테이션 (Compile-Time Annotation)** <br>
컴파일러가 코드를 분석하는 과정에서 사용되며, 컴파일 후에는 코드에서 사라짐.

**예제**<br>
```@Override``` → 부모 클래스의 메서드를 올바르게 재정의했는지 검사<br>
```@Deprecated``` → 더 이상 사용되지 않는 메서드임을 표시
```java
class Parent {
    void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {
    @Override
    void display() {  // 올바르게 오버라이드되었는지 검사
        System.out.println("Child");
    }
}
```

**런타임 애노테이션 (Runtime Annotation)** <br>

프로그램 실행 중에도 유지되며, Reflection API를 사용하여 읽고 활용할 수 있음.<br>
Spring Boot에서는 런타임 애노테이션을 활용하여 자동으로 빈을 등록하거나, 트랜잭션을 관리하는 등의 작업을 수행함.<br>

**예제**<br>
```@Component``` → Spring 컨테이너에서 자동으로 빈을 등록<br>
```@Transactional``` → 데이터베이스 트랜잭션을 관리
```java

@Retention(RetentionPolicy.RUNTIME)  // 런타임까지 유지되는 애노테이션
@Target(ElementType.TYPE)
@interface CustomAnnotation {
    String value();
}

@CustomAnnotation(value = "ExampleClass")
class ExampleClass {
}

public class AnnotationProcessor {
    public static void main(String[] args) {
        Class<?> clazz = ExampleClass.class;
        CustomAnnotation annotation = clazz.getAnnotation(CustomAnnotation.class);
        System.out.println("애노테이션 값: " + annotation.value());
    }
}
```
실행 결과:<br>
```java
애노테이션 값: ExampleClass
```
위 코드는 @CustomAnnotation이라는 사용자 정의 애노테이션을 만들고, 런타임 중에 해당 애노테이션 값을 읽어 출력하는 예제이다.<br>
Spring Boot에서는 이러한 런타임 애노테이션을 활용하여 동적으로 애플리케이션을 설정하고 관리할 수 있다.

-------------
### 애노테이션의 기본 구조
애노테이션은 Java에서 @interface 키워드를 사용하여 정의된다.<br>
애노테이션에는 속성(Annotation Attribute) 을 지정할 수 있으며, 기본값을 설정할 수도 있다.

다음은 기본적인 애노테이션의 구조를 나타낸 코드이다.
```java
public @interface CustomAnnotation {
    String name();  // 필수 속성 (기본값 없음)
    int level() default 1;  // 기본값을 1로 설정
}
```
위와 같이 애노테이션을 정의하면, 이를 특정 클래스에 적용할 수 있다.
```java
@CustomAnnotation(name = "Admin", level = 5)
class User {
}
```
애노테이션을 활용하면 클래스나 메서드에 추가적인 정보를 부여할 수 있으며,<br>
이 정보를 기반으로 Spring Boot에서는 빈 자동 등록, 트랜잭션 관리, AOP 적용 등 다양한 기능을 수행할 수 있다.

-------------
### Spring Boot에서 애노테이션이 중요한 이유
Spring Boot는 전통적인 Java 개발 방식과 비교했을 때 애노테이션을 적극적으로 활용하여 설정을 자동화하는 것이 특징이다.<br>
과거에는 XML을 이용하여 모든 설정을 정의해야 했지만,<br>
Spring Boot에서는 애노테이션만 추가하면 자동으로 설정을 적용할 수 있다.

예를 들어, 과거에는 빈(Bean)을 XML에서 다음과 같이 설정해야 했다.
```java
<bean id="userService" class="com.example.UserService" />
```

하지만 Spring Boot에서는 단순히 @Service 애노테이션을 추가하는 것만으로도 같은 효과를 얻을 수 있다.
```java
@Service
public class UserService {
}
```
이처럼 애노테이션을 활용하면 코드를 더욱 간결하고 직관적으로 만들 수 있으며, 유지보수성을 높일 수 있다.

------------
### 1. 애플리케이션 구성 및 자동 설정 (Auto Configuration)
Spring Boot의 가장 큰 장점 중 하나는 자동 설정(Auto Configuration) 이다.<br>
이를 가능하게 하는 핵심 애노테이션이 바로 ```@SpringBootApplication```이다.
```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```
위 코드에서 @SpringBootApplication 애노테이션은 사실 여러 개의 애노테이션을 조합한 것이다.

```@SpringBootConfiguration```: 애플리케이션의 설정 클래스로 지정<br>
```@EnableAutoConfiguration```: 자동 설정을 활성화<br>
```@ComponentScan```: 특정 패키지 이하의 빈(Bean)을 자동으로 검색<br>

즉, ```@SpringBootApplication``` 하나만 추가해도 자동 설정 및 빈 등록이 활성화되며,<br>
개발자는 복잡한 설정 없이 애플리케이션을 빠르게 개발할 수 있다.

-------------
### 2. 빈(Bean) 관리 및 의존성 주입 (Dependency Injection)
Spring Boot는 의존성 주입(DI, Dependency Injection) 을 기반으로 동작하며,<br>
이를 위해 @Component, @Service, @Repository 등의 애노테이션을 사용한다.
```java
@Service
public class UserService {
    public String getUser() {
        return "사용자 정보 반환";
    }
}
```
위 코드에서 @Service 애노테이션을 사용하면,<br>
Spring Boot가 UserService 클래스를 빈(Bean)으로 등록하고 자동으로 관리한다.

이렇게 등록된 빈은 @Autowired를 사용하여 다른 클래스에서 주입받아 사용할 수 있다.
@RestController
public class UserController {

    private final UserService userService;

    @Autowired
    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping("/user")
    public String getUser() {
        return userService.getUser();
    }
}
@RestController: REST API 컨트롤러로 동작하도록 설정
@Autowired: UserService 빈을 자동 주입
이처럼 Spring Boot의 애노테이션을 활용하면 객체 간의 의존성을 자동으로 관리할 수 있다.
