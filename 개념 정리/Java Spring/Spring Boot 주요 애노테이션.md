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
이를 위해 ```@Component```, ```@Service```,```@Repository``` 등의 애노테이션을 사용한다.
```java
@Service
public class UserService {
    public String getUser() {
        return "사용자 정보 반환";
    }
}
```
위 코드에서 ```@Service``` 애노테이션을 사용하면,<br>
Spring Boot가 ```UserService``` 클래스를 빈(Bean)으로 등록하고 자동으로 관리한다.

이렇게 등록된 빈은 ```@Autowired```를 사용하여 다른 클래스에서 주입받아 사용할 수 있다.
```java
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
```
```@RestController```: REST API 컨트롤러로 동작하도록 설정<br>
```@Autowired```: UserService 빈을 자동 주입<br>
이처럼 Spring Boot의 애노테이션을 활용하면 객체 간의 의존성을 자동으로 관리할 수 있다.

------------------
### 3. 데이터베이스 연동 및 트랜잭션 관리
Spring Boot에서 데이터베이스와의 연동을 위해 Spring Data JPA를 사용할 경우,<br>
애노테이션을 통해 간단하게 리포지토리(Repository)를 정의할 수 있다.
```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
}
```
```@Repository``` : 데이터 접근 계층(DAO)을 나타내며, Spring이 자동으로 인식하도록 함<br>
```JpaRepository<User, Long>``` : JPA의 기본 기능을 제공하며, 별도의 SQL 없이 CRUD 지원

또한, 데이터베이스 트랜잭션을 관리하기 위해 @Transactional 애노테이션을 사용할 수 있다.
```java
@Service
public class OrderService {

    private final OrderRepository orderRepository;

    @Autowired
    public OrderService(OrderRepository orderRepository) {
        this.orderRepository = orderRepository;
    }

    @Transactional
    public void createOrder(Order order) {
        orderRepository.save(order);
        // 예외 발생 시 자동으로 롤백됨
    }
}
```
```@Transactional```: 트랜잭션을 관리하며, 예외가 발생하면 자동으로 롤백<br>
이러한 애노테이션 덕분에 데이터베이스 연동 및 트랜잭션 처리를 간단하게 구현할 수 있다.

-------------
### 4. RESTful API 및 요청 처리
Spring Boot에서는 RESTful API를 쉽게 구현할 수 있도록
@RestController, @RequestMapping, @GetMapping, @PostMapping 등의 애노테이션을 제공한다.

@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public String getUser(@PathVariable Long id) {
        return "User ID: " + id;
    }
}
위 코드에서 사용하는 애노테이션의 역할은 다음과 같다.

```@RestController```: 해당 클래스를 REST 컨트롤러로 지정<br>
```@RequestMapping("/users")```: users 경로로 들어오는 요청을 처리<br>
```@GetMapping("/{id}")```: GET /users/{id} 요청을 해당 메서드와 매핑<br>
```@PathVariable```: URL 경로 변수 값을 메서드 파라미터로 전달<br>

이처럼 Spring Boot의 애노테이션을 활용하면 REST API를 간결하게 정의할 수 있다.

-----------------
### 5. AOP(Aspect-Oriented Programming) 및 공통 기능 적용
Spring Boot에서는 **AOP(Aspect-Oriented Programming)** 를 활용하여<br>
로깅, 보안, 성능 모니터링 등의 공통 기능을 적용할 수 있다.

예를 들어, ```@Aspect```와 ```@Before```를 사용하여 특정 메서드가 실행되기 전에 로그를 남길 수 있다.
```java
@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.service.*.*(..))")
    public void logBeforeMethod() {
        System.out.println("메서드 실행 전 로그 출력");
    }
}
```
```@Aspect```: 해당 클래스가 AOP 기능을 수행하는 Aspect 클래스임을 지정<br>
```@Before("execution(* com.example.service.*.*(..))")```:com.example.service 패키지의 모든 메서드 실행 전에 로그 출력

이러한 AOP 애노테이션을 사용하면 코드를 수정하지 않고도 공통 기능을 추가할 수 있다.

----------
### Spring Boot에서 애노테이션의 역할 요약
Spring Boot의 애노테이션은 단순한 코드 주석이 아니라,<br>
애플리케이션의 동작을 정의하고 설정을 자동화하는 핵심적인 요소이다.

**자동 설정 (Auto Configuration)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@SpringBootApplication을 사용하여 자동으로 설정을 활성화

**빈(Bean) 등록 및 의존성 주입**<br>
@Component, @Service, @Repository 등을 활용하여 자동 빈 관리<br>
@Autowired를 사용하여 의존성을 자동 주입

**데이터베이스 연동 및 트랜잭션 관리**<br>
@Repository를 통해 데이터 접근 계층 자동 설정<br>
@Transactional을 사용하여 데이터베이스 트랜잭션 관리

**RESTful API 및 요청 처리**<br>
@RestController, @RequestMapping, @GetMapping 등을 활용하여 REST API 개발

**AOP 및 공통 기능 적용**<br>
@Aspect, @Before를 활용하여 로깅, 보안, 성능 모니터링 등의 기능 적용<br>

Spring Boot의 애노테이션을 이해하고 활용하면 더욱 효율적인 애플리케이션 개발이 가능하다

---------------------
## 2. 컨트롤러 계층의 주요 애노테이션
Spring Boot의 웹 애플리케이션에서 컨트롤러(Controller) 계층은 사용자의 요청을 처리하고, 응답을 반환하는 역할을 담당한다.<br>
Spring MVC 패턴에서 컨트롤러는 비즈니스 로직을 수행하는 서비스(Service) 계층과 데이터베이스를 처리하는 리포지토리(Repository) 계층을 연결하는 핵심적인 역할을 한다.

Spring Boot에서는 컨트롤러를 효율적으로 정의하고 요청을 매핑할 수 있도록 여러 개의 애노테이션을 제공하며,<br>
이러한 애노테이션들은 코드를 간결하게 유지하면서도 가독성과 유지보수성을 높이는 역할을 한다.

### 1. @Controller - MVC 컨트롤러 정의
Spring MVC에서 가장 기본적인 컨트롤러 역할을 수행하는 애노테이션은 ```@Controller이다.```<br><br>
이 애노테이션은 클래스를 컨트롤러로 인식하고, 해당 클래스의 메서드가 웹 요청을 처리하도록 설정한다.
```java
@Controller
public class HomeController {

    @GetMapping("/")
    public String home() {
        return "home"; // home.html 또는 home.jsp 뷰 반환
    }
}
```
위 코드에서 @Controller는 Spring이 해당 클래스를 웹 컨트롤러로 인식하도록 지정한다.<br>
그리고 @GetMapping("/")을 통해 루트 경로("/")에 대한 요청을 처리한다.

하지만 **@Controller만 사용하면 메서드의 반환값은 기본적으로 "뷰(view) 이름"으로 인식된다.** <br>
따라서 템플릿 엔진(Thymeleaf, JSP 등)과 함께 사용할 때 적절하다.

--------------------
### 2. @RestController - REST API 컨트롤러 정의
```@Controller```는 뷰를 반환하는 용도로 사용되지만,<br>
RESTful API를 구현할 때는 @RestController를 사용하는 것이 일반적이다.
```java
@RestController
public class ApiController {

    @GetMapping("/api/message")
    public String getMessage() {
        return "Hello, REST API!";
    }
}
```
위 코드에서 ```@RestController```는 컨트롤러가 문자열 데이터를 직접 반환하도록 설정한다.<br>
즉, "Hello, REST API!"라는 응답이 JSON 형식으로 클라이언트에게 전달된다.

@RestController는 내부적으로 @Controller와 @ResponseBody를 포함하고 있어<br>
모든 메서드의 반환값이 자동으로 JSON 또는 XML과 같은 응답 본문(Response Body)으로 처리된다.

-----------------
### 3. @RequestMapping - 요청 URL 매핑
@RequestMapping 애노테이션은 클래스 또는 메서드에 특정 URL을 매핑하는 역할을 한다.
```java
@RestController
@RequestMapping("/api")
public class UserController {

    @GetMapping("/user")
    public String getUser() {
        return "User information";
    }
}
```
위 코드에서 @RequestMapping("/api")는 해당 컨트롤러의 모든 엔드포인트가 "/api"를 포함하도록 설정한다.<br>
즉, /api/user로 요청하면 "User information" 응답이 반환된다.

```@RequestMapping```은 단순한 URL 매핑뿐만 아니라 요청 방식(HTTP Method)도 지정할 수 있다.
```java
@RequestMapping(value = "/users", method = RequestMethod.GET)
public String getUsers() {
    return "User List";
}
```
하지만, Spring Boot에서는 HTTP 메서드를 처리하는 전용 애노테이션(@GetMapping, @PostMapping 등)이 존재하기 때문에
요청 방식이 명확한 경우 @RequestMapping보다 전용 애노테이션을 사용하는 것이 권장된다.

----------------
### 4. HTTP 메서드 매핑 애노테이션
Spring Boot에서는 HTTP 요청 방식(메서드)에 따라 별도의 매핑 애노테이션을 제공한다.

```@GetMapping``` - GET 요청을 처리<br>
```@PostMapping``` - POST 요청을 처리<br>
```@PutMapping``` - PUT 요청을 처리<br>
```@DeleteMapping``` - DELETE 요청을 처리<br>
이러한 애노테이션을 활용하면 보다 간결하게 RESTful API를 구현할 수 있다.
```java
@RestController
@RequestMapping("/products")
public class ProductController {

    @GetMapping("/{id}")
    public String getProduct(@PathVariable Long id) {
        return "Product ID: " + id;
    }

    @PostMapping
    public String createProduct(@RequestBody String product) {
        return "Product created: " + product;
    }

    @PutMapping("/{id}")
    public String updateProduct(@PathVariable Long id, @RequestBody String product) {
        return "Product " + id + " updated: " + product;
    }

    @DeleteMapping("/{id}")
    public String deleteProduct(@PathVariable Long id) {
        return "Product " + id + " deleted";
    }
}
```
위 코드에서 각 애노테이션은 다음과 같은 역할을 한다.

```@GetMapping("/{id}")``` → 특정 ID의 제품 정보를 조회<br>
```@PostMapping``` → 새로운 제품을 생성<br>
```@PutMapping("/{id}")``` → 특정 ID의 제품 정보를 업데이트<br>
```@DeleteMapping("/{id}")``` → 특정 ID의 제품을 삭제<br>
이처럼 @RequestMapping 대신 HTTP 메서드별 애노테이션을 사용하면 코드의 가독성이 높아지고 직관적으로 이해할 수 있다.

------------------
### 컨트롤러 계층에서 애노테이션의 활용 요약
컨트롤러 계층은 사용자의 요청을 처리하고 응답을 반환하는 핵심적인 역할을 하며,<br>
Spring Boot에서는 다음과 같은 애노테이션을 활용하여 컨트롤러를 정의하고 요청을 처리한다.

**컨트롤러 정의**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Controller → 뷰(View) 반환을 위한 MVC 컨트롤러<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@RestController → REST API 응답을 위한 컨트롤러

**요청 URL 매핑**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@RequestMapping → 클래스 또는 메서드에 특정 URL 매핑<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@GetMapping, @PostMapping, @PutMapping, @DeleteMapping → HTTP 요청 방식에 따라 매핑

이러한 애노테이션을 활용하면 간결한 코드로 가독성이 높은 컨트롤러를 작성할 수 있으며,<br>
Spring Boot의 강력한 요청 처리 기능을 효율적으로 사용할 수 있다.

---------------------
## 서비스 계층의 주요 애노테이션
서비스(Service) 계층은 애플리케이션에서 비즈니스 로직을 처리하는 핵심적인 역할을 수행한다.<br>
이 계층은 컨트롤러와 데이터 접근 계층(Repository) 사이에서 동작하며, 비즈니스 로직을 캡슐화하여 코드의 재사용성과 유지보수성을 높이는 역할을 한다.

Spring Boot에서는 서비스 계층을 명확히 정의하고 관리하기 위해 @Service 애노테이션을 제공한다.<br>
또한, 서비스 계층에서 종종 활용되는 트랜잭션 관리 애노테이션(@Transactional) 에 대해서도 함께 알아보자.

----------------
### @Service - 서비스 클래스 정의
```@Service``` 애노테이션은 Spring이 해당 클래스를 서비스 계층의 컴포넌트로 인식하고 관리할 수 있도록 설정한다.<br>
Spring 컨테이너는 ```@Service```가 붙은 클래스를 자동으로 빈(Bean)으로 등록하고, 필요한 곳에서 이를 주입하여 사용할 수 있도록 한다.
```java
import org.springframework.stereotype.Service;

@Service
public class UserService {

    public String getUserInfo(Long id) {
        return "User Info for ID: " + id;
    }
}
```
위 코드에서 ```@Service```는 UserService 클래스를 Spring의 서비스 빈으로 등록한다.<br>
이제 컨트롤러에서 UserService를 의존성 주입을 통해 사용할 수 있다.
```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/users")
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping("/{id}")
    public String getUser(@PathVariable Long id) {
        return userService.getUserInfo(id);
    }
}
```
여기서 UserService는 생성자 주입 방식으로 컨트롤러에 주입되었으며,<br>
컨트롤러는 ```userService.getUserInfo(id)```를 호출하여 사용자 정보를 조회하는 역할을 수행한다.

-------------------
### @Transactional - 트랜잭션 관리
서비스 계층에서는 데이터베이스와 직접적인 연산을 수행할 일이 많으며,<br>
이때 트랜잭션(Transaction)을 관리하는 것이 필수적이다.<br>
Spring Boot에서는 트랜잭션을 손쉽게 관리할 수 있도록 @Transactional 애노테이션을 제공한다.

**트랜잭션(Transaction)이란?**<br>
+ 여러 개의 데이터베이스 연산을 하나의 단위로 묶어 관리하는 개념이다.<br>
+ 트랜잭션 내에서 하나라도 실패하면 전체 작업을 취소(rollback)하여 데이터 정합성을 유지한다.<br>
+ 트랜잭션이 정상적으로 완료되면 commit을 수행하여 변경 사항을 확정한다.

다음은 @Transactional을 활용한 서비스 계층 코드 예제이다.
```java
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

@Service
public class AccountService {

    private final AccountRepository accountRepository;

    public AccountService(AccountRepository accountRepository) {
        this.accountRepository = accountRepository;
    }

    @Transactional
    public void transferMoney(Long fromAccountId, Long toAccountId, double amount) {
        Account fromAccount = accountRepository.findById(fromAccountId)
                .orElseThrow(() -> new RuntimeException("송금 계좌를 찾을 수 없습니다."));
        Account toAccount = accountRepository.findById(toAccountId)
                .orElseThrow(() -> new RuntimeException("입금 계좌를 찾을 수 없습니다."));

        if (fromAccount.getBalance() < amount) {
            throw new RuntimeException("잔액이 부족합니다.");
        }

        fromAccount.withdraw(amount);
        toAccount.deposit(amount);

        accountRepository.save(fromAccount);
        accountRepository.save(toAccount);
    }
}
```
위 코드에서 @Transactional이 적용된 transferMoney 메서드는 모든 데이터베이스 연산이 성공해야만 변경 사항이 적용된다.<br>
즉, 송금 계좌에서 출금한 후 입금 계좌에 입금하기까지의 과정에서 오류가 발생하면, 이전 작업도 자동으로 취소(rollback)되어 데이터의 일관성을 유지할 수 있다.

------------------------
###  @Service와 @Transactional을 함께 사용할 때 주의할 점
**서비스 클래스의 메서드에서 다른 내부 메서드를 호출하면 트랜잭션이 정상적으로 동작하지 않을 수 있다.** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Transactional이 선언된 메서드를 같은 클래스의 내부에서 호출하면, Spring 프록시(proxy)가 적용되지 않아 트랜잭션이 제대로 동작하지 않을 가능성이 높다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;해결 방법: 자신이 아닌 다른 빈을 통해 메서드를 호출해야 한다.

**트랜잭션이 필요한 메서드는 퍼블릭(public) 접근자로 선언해야 한다.** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Transactional은 기본적으로 Spring의 AOP(Aspect-Oriented Programming) 방식으로 동작하며,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Spring이 관리하는 프록시(proxy) 객체를 통해 트랜잭션을 적용한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;따라서 메서드가 private이거나 같은 클래스 내에서 직접 호출되면 트랜잭션이 적용되지 않는다.<br>

**트랜잭션의 전파(Propagation) 설정을 고려해야 한다.** <br>
+ 트랜잭션은 전파(Propagation) 옵션을 설정할 수 있으며, 대표적인 값은 다음과 같다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;REQUIRED (기본값) : 기존 트랜잭션이 있으면 참여하고, 없으면 새로운 트랜잭션을 생성한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;REQUIRES_NEW : 기존 트랜잭션을 무시하고, 항상 새로운 트랜잭션을 생성한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SUPPORTS : 기존 트랜잭션이 있으면 참여하고, 없으면 트랜잭션 없이 실행한다.

다음은 @Transactional의 전파 옵션을 설정하는 예제이다.
```java
@Transactional(propagation = Propagation.REQUIRES_NEW)
public void updateAccount(Account account) {
    accountRepository.save(account);
}
```
위 설정에서는 항상 새로운 트랜잭션을 생성하여 updateAccount 메서드를 실행한다.<br>
이렇게 하면 부모 트랜잭션이 롤백되더라도 이 메서드에서 수행된 작업은 독립적으로 커밋될 수 있다

------------------
### 서비스 계층에서 애노테이션의 활용 요약
**서비스 계층을 정의하는 애노테이션**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Service → 비즈니스 로직을 처리하는 서비스 클래스를 정의<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Transactional → 트랜잭션 처리를 적용하여 데이터의 일관성을 유지

**트랜잭션 관리**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Transactional을 사용하여 트랜잭션을 자동으로 관리<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;내부 메서드 호출 시 트랜잭션이 정상적으로 동작하지 않을 가능성이 있으므로 주의<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;트랜잭션 전파(Propagation) 옵션을 활용하여 원하는 트랜잭션 정책을 설정 가능

이처럼 ```@Service```와``` @Transactional```을 적절히 활용하면,<br>
서비스 계층에서 비즈니스 로직을 모듈화하고 데이터의 정합성을 유지하는 효과적인 구조를 만들 수 있다.

---------------
## 리포지토리 계층의 주요 애노테이션
리포지토리(Repository) 계층은 데이터베이스와 직접적으로 상호작용하는 계층으로,<br>
애플리케이션에서 데이터를 저장, 조회, 수정, 삭제하는 기능을 담당한다.

Spring Boot에서는 이 계층을 효율적으로 관리하기 위해 ```@Repository``` 애노테이션을 제공하며,<br>
Spring Data JPA를 활용하면 별도의 구현 없이도 CRUD 메서드를 사용할 수 있다.<br>
또한, 리포지토리 계층에서 트랜잭션 관리를 위해 ```@Transactional``` 애노테이션이 함께 사용되는 경우가 많다.

-----------------
### @Repository - 데이터 접근 계층을 위한 애노테이션
@Repository 애노테이션은 DAO(Data Access Object) 클래스에서 사용되며,<br>
Spring이 해당 클래스를 빈(Bean)으로 관리하도록 설정한다.

이 애노테이션의 주요 역할은 다음과 같다.<br>
+ 데이터 액세스 계층(DAO)으로 인식하여 관리
+ JPA, JDBC, MyBatis 등의 데이터 액세스 기술과 결합 가능
+ Spring이 발생하는 특정 예외를 DataAccessException으로 변환하여 처리

다음은 ```@Repository``` 애노테이션을 적용한 기본적인 예제이다.
```java
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;
import java.util.Optional;

@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    Optional<User> findByUsername(String username);
}
```
위 코드는 ```JpaRepository<User, Long>```를 상속받아,<br>
User 엔티티를 기반으로 CRUD 연산을 수행하는 리포지토리 클래스를 정의한다.

이제 서비스 계층에서 ```UserRepository```를 활용하면,<br>
DB에 접근하는 로직을 직접 구현할 필요 없이 Spring Data JPA가 자동으로 처리한다.
```java
import org.springframework.stereotype.Service;
import java.util.Optional;

@Service
public class UserService {

    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public User findUserByUsername(String username) {
        return userRepository.findByUsername(username)
                .orElseThrow(() -> new RuntimeException("사용자를 찾을 수 없습니다."));
    }
}
```
여기서 ```findByUsername``` 메서드는 JPA의 메서드 네이밍 규칙을 따르기만 하면 자동으로 구현된다.<br>
즉, findBy필드명 형식으로 선언하면 Spring Data JPA가 이를 해석하여 쿼리를 자동 생성한다.

--------------
### @Repository와 예외 변환 (Spring 예외 처리 기능)
Spring에서 ```@Repository```를 사용할 때의 중요한 특징 중 하나는 예외 변환(Exception Translation) 이다.<br>
Spring은 SQL 또는 JPA 관련 예외가 발생했을 때,<br>
이를 Spring의 공통 예외 클래스(DataAccessException)로 변환하여 일관되게 처리할 수 있도록 해준다.

예를 들어, JDBC를 사용하여 직접 데이터베이스에 접근할 경우,<br>
```SQLException```이 발생할 수 있다.
하지만 ```@Repository```가 적용된 클래스에서 예외가 발생하면,
Spring이 이를 자동으로 ```DataAccessException``` 계열의 예외로 변환한다.

예제
```java
try {
    userRepository.findByUsername("testUser")
            .orElseThrow(() -> new RuntimeException("사용자를 찾을 수 없습니다."));
} catch (DataAccessException e) {
    // Spring이 데이터 액세스 관련 예외를 변환하여 처리 가능하게 해줌
    throw new RuntimeException("데이터베이스 접근 중 오류가 발생했습니다.", e);
}
```
위 코드에서 ```DataAccessException```을 캐치하면,<br>
데이터베이스 연결 문제, SQL 구문 오류, 무결성 제약 조건 위반 등 다양한 데이터베이스 관련 오류를 한 곳에서 처리할 수 있다.<br>
이러한 예외 변환 기능은 Spring이 제공하는 큰 장점 중 하나이다.

-----------------
### Spring Data JPA와 @Repository의 결합
Spring Boot에서 리포지토리 계층을 더 효율적으로 관리하기 위해,<br>
```@Repository```와 함께 Spring Data JPA를 활용하면 자동으로 CRUD 메서드를 제공받을 수 있다.

Spring Data JPA를 사용할 경우,<br>
인터페이스만 선언하면 Spring이 구현체를 자동 생성한다.

기본적인 CRUD 기능을 제공하는 인터페이스 예제
```java
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface ProductRepository extends JpaRepository<Product, Long> {
}
```
위 인터페이스는 다음과 같은 기능을 자동으로 제공한다.
|메서드|기능|
|:---|:---|
|```save(T entity)```|엔티티 저장 및 업데이트|
|```findById(ID id)```|ID로 엔티티 조회|
|```findAll()```|모든 엔티티 조회|
|```deleteById(ID id)```|ID로 엔티티 삭제|

즉, ```ProductRepository```는 별도의 구현 없이도 위와 같은 CRUD 기능을 사용할 수 있다.
------------------
### 커스텀 쿼리 메서드 작성
Spring Data JPA는 기본적인 CRUD 메서드뿐만 아니라,<br>
메서드 네이밍 규칙을 기반으로 사용자 지정 쿼리 메서드를 생성할 수도 있다.

예를 들어, 특정 카테고리에 속하는 모든 상품을 조회하는 메서드를 정의해보자.
```java
import org.springframework.data.jpa.repository.JpaRepository;
import java.util.List;

public interface ProductRepository extends JpaRepository<Product, Long> {
    List<Product> findByCategory(String category);
}
```
위 코드에서는 ```findByCategory(String category)```라는 메서드를 선언했을 뿐이지만,
Spring Data JPA가 자동으로 ```SELECT * FROM product WHERE category = ?```SQL 쿼리를 생성해준다.

서비스 계층에서 이를 호출하면, 특정 카테고리에 해당하는 상품 목록을 쉽게 가져올 수 있다.
```java
import org.springframework.stereotype.Service;
import java.util.List;

@Service
public class ProductService {

    private final ProductRepository productRepository;

    public ProductService(ProductRepository productRepository) {
        this.productRepository = productRepository;
    }

    public List<Product> getProductsByCategory(String category) {
        return productRepository.findByCategory(category);
    }
}
```
이처럼 리포지토리 계층에서는 SQL을 직접 작성하지 않고도 쿼리 메서드만으로 원하는 데이터를 쉽게 조회할 수 있다.

----------------------
### @Repository를 사용할 때 주의할 점
**Spring Data JPA 사용 시 별도로 @Repository를 선언하지 않아도 된다.** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JpaRepository를 상속하면 Spring이 자동으로 빈(Bean)으로 등록하므로,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;필수적으로 @Repository를 붙이지 않아도 동작한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;하지만 명시적으로 @Repository를 선언하면 Spring이 예외 변환 기능을 제공하기 때문에,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JDBC, MyBatis 등 다른 데이터 접근 기술을 사용할 때는 @Repository를 반드시 붙이는 것이 좋다.

**리포지토리 인터페이스는 비즈니스 로직을 포함하면 안 된다.** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;리포지토리는 데이터 접근과 관련된 역할만 수행해야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;비즈니스 로직은 서비스 계층에서 처리해야 하며,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;리포지토리는 단순히 데이터를 저장하고 불러오는 역할을 맡아야 한다.

**트랜잭션과 함께 사용할 때 주의해야 한다.** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Transactional을 서비스 계층에서 설정하는 것이 일반적이며,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;리포지토리 계층에서 직접 트랜잭션을 관리하지 않는 것이 좋다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터의 일관성을 유지하려면 서비스 계층에서 트랜잭션을 관리하고,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;리포지토리는 데이터 접근만 담당하도록 설계하는 것이 권장된다.

------------------
## 의존성 주입의 개념
Spring Boot는 의존성 주입(Dependency Injection, DI) 개념을 활용하여<br>
객체 간의 의존 관계를 효율적으로 관리할 수 있도록 한다.<br>
의존성 주입이란 클래스 내부에서 직접 객체를 생성하지 않고, 외부에서 필요한 객체를 주입받아 사용하는 방식을 의미한다.

----------------
