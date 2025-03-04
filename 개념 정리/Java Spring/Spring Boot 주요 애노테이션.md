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
### 의존성 주입이 필요한 이유
객체를 직접 생성하는 방식과 의존성 주입을 사용하는 방식의 차이를 이해하기 위해,<br>
다음과 같은 예제를 살펴보자.

객체를 직접 생성하는 방식
```java
public class UserService {
    private UserRepository userRepository = new UserRepository();

    public String getUserInfo(Long id) {
        return userRepository.findUserById(id);
    }
}
```
위 코드에서 ```UserService```는 ```UserRepository```를 직접 생성하고 있다.<br>
이 방식에는 다음과 같은 문제점이 있다.

**유연성이 떨어진다**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;UserRepository가 변경되면, 이를 사용하는 모든 클래스에서 변경해야 한다.

**테스트가 어렵다**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;UserRepository를 직접 생성하므로, 테스트 시 가짜 객체(Mock 객체)를 주입할 수 없다.

**확장성이 부족하다**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, UserRepository의 구현체를 JpaUserRepository에서 JdbcUserRepository로 변경하려면,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;모든 코드에서 직접 변경이 필요하다.

--------------
### 의존성 주입을 사용하는 방식
위 문제를 해결하려면 의존성을 직접 생성하는 것이 아니라, 외부에서 주입받는 방식으로 변경해야 한다.
```java
public class UserService {
    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public String getUserInfo(Long id) {
        return userRepository.findUserById(id);
    }
}
```
이제 UserRepository는 외부에서 생성되어 주입된다.<br>
이를 통해 구현체를 변경할 때 UserService를 수정하지 않아도 된다.<br>
또한, 테스트 시 Mock 객체를 주입하여 독립적으로 테스트할 수도 있다.

Spring Boot에서는 이러한 의존성 주입을 자동으로 수행하며,<br>
이를 위해 다양한 의존성 주입 방식을 제공한다.

------------
### Spring Boot에서의 의존성 주입 방식
Spring Boot에서 지원하는 대표적인 의존성 주입 방식은 다음과 같다.

+ **생성자 주입 (Constructor Injection)**
+ **필드 주입 (Field Injection)**
+ **메서드 주입 (Setter Injection)**

----------------
### 생성자 주입 (Constructor Injection)
생성자 주입은 생성자를 이용하여 의존성을 주입하는 방식이다.
```java
import org.springframework.stereotype.Service;

@Service
public class UserService {

    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public String getUserInfo(Long id) {
        return userRepository.findUserById(id);
    }
}
```
**특징**<br>
final 키워드를 사용할 수 있어 불변성을 유지할 수 있다.<br>
UserService 객체가 생성될 때 의존성이 반드시 주입되어야 하므로, NPE(NullPointerException) 발생 가능성을 줄일 수 있다.<br>
Spring Boot 4.3 이후 버전에서는 @Autowired를 명시하지 않아도 자동으로 의존성을 주입한다.

**장점**<br>
객체가 생성될 때 의존성이 명확하게 주입되므로, 안정성이 높다.<br>
테스트 시에도 Mock 객체를 쉽게 주입할 수 있다.<br>
필수적인 의존성이 없으면 컴파일 오류가 발생하므로, 런타임 오류를 방지할 수 있다.

**단점**<br>
의존성이 많아질 경우 생성자가 길어질 수 있다.<br>
순환 의존성이 발생하면 해결하기 어려울 수 있다.<br>
(순환 의존성이란, A → B → A 같은 구조로 서로가 서로를 참조하는 상황을 의미한다.)

---------------
### 필드 주입 (Field Injection)
필드 주입은 클래스의 필드에 직접 @Autowired를 선언하여 의존성을 주입하는 방식이다.
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public String getUserInfo(Long id) {
        return userRepository.findUserById(id);
    }
}
```
**특징**<br>
필드에 @Autowired를 추가하면, Spring이 자동으로 의존성을 주입한다.<br>
가장 간단한 방법이며, 코드가 짧고 직관적이다.<br>

**장점**<br>
코드가 간결하며, 유지보수가 쉽다.<br>
Spring이 자동으로 의존성을 주입해주므로 설정이 간단하다.

**단점**<br>
final 키워드를 사용할 수 없으므로, 불변성을 유지할 수 없다.<br>
테스트 시 Mock 객체를 주입하려면 Reflection을 사용해야 하므로, 테스트 코드가 복잡해진다.<br>
순환 의존성 문제가 발생할 가능성이 높다.

-----------------------------
### 메서드 주입 (Setter Injection)
메서드 주입은 Setter 메서드를 통해 의존성을 주입하는 방식이다.
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class UserService {

    private UserRepository userRepository;

    @Autowired
    public void setUserRepository(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public String getUserInfo(Long id) {
        return userRepository.findUserById(id);
    }
}
```
**특징**<br>
@Autowired를 Setter 메서드에 선언하여 주입한다.<br>
선택적인 의존성 주입이 가능하므로, 특정 경우에만 의존성을 주입할 수도 있다.

**장점**<br>
런타임 중에 의존성을 변경할 수 있어 유연성이 높다.<br>
순환 의존성이 발생할 경우, 해결이 비교적 쉽다.

**단점**
필수 의존성을 보장할 수 없다.<br>
(의존성이 주입되지 않은 상태에서 메서드가 호출될 가능성이 있다.)<br>
객체 생성 이후에 Setter가 호출되므로, 객체의 일관성을 유지하기 어렵다.

-------------------
## 주요 의존성 주입 애노테이션
Spring Boot에서는 객체 간의 의존 관계를 관리하기 위해 다양한 애노테이션을 제공한다.<br>
이러한 애노테이션들은 개발자가 직접 객체를 생성하고 관리하는 부담을 줄이고,<br>
Spring 컨테이너가 자동으로 객체를 주입하도록 돕는다.

이번 섹션에서는 Spring Boot에서 의존성 주입을 위해 사용되는 주요 애노테이션을 살펴본다.

-------------
### @Autowired – 자동으로 빈(Bean) 주입
@Autowired 애노테이션은 가장 많이 사용되는 의존성 주입 애노테이션 중 하나다.<br>
이 애노테이션을 사용하면 Spring이 자동으로 적절한 빈을 찾아서 주입해준다.
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class UserService {

    private final UserRepository userRepository;

    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public String getUserInfo(Long id) {
        return userRepository.findUserById(id);
    }
}
```
**특징**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Autowired는 Spring이 자동으로 적절한 빈을 찾아서 주입해준다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;생성자, 필드, Setter 메서드에서 사용할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Spring Boot 4.3 이후 버전에서는 생성자가 하나만 존재할 경우 @Autowired를 생략해도 자동으로 주입된다.

**어떤 방식이 가장 좋은가?** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;생성자 주입을 권장: Spring에서는 생성자 주입을 가장 권장하며, 이를 사용하면 불변성을 유지할 수 있고 NullPointerException을 방지할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;필드 주입은 피하는 것이 좋음: 필드 주입을 사용하면 테스트가 어렵고, 클래스의 의존성이 명확하지 않다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Setter 주입은 선택적으로 사용: 특정 상황에서만 Setter 주입을 사용할 수 있지만, 필수 의존성의 경우에는 사용하지 않는 것이 좋다.

-------------
### @Qualifier – 동일한 타입의 여러 빈 중 특정 빈을 선택
```@Autowired```는 기본적으로 타입을 기준으로 빈을 찾아서 주입하지만,<br>
동일한 타입의 빈이 여러 개 존재할 경우 어떤 빈을 주입할지 명확하지 않다.<br>
이럴 때 ```@Qualifier``` 를 사용하여 특정 빈을 명시적으로 선택할 수 있다.
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Service;

@Service
public class UserService {

    private final UserRepository userRepository;

    @Autowired
    public UserService(@Qualifier("jpaUserRepository") UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public String getUserInfo(Long id) {
        return userRepository.findUserById(id);
    }
}
```
그리고 같은 타입의 두 개 이상의 빈이 존재하는 경우,
각 빈에 ```@Component``` 또는 ```@Repository```를 사용하면서 ```@Qualifier```에 사용할 이름을 지정해야 한다.
```java
import org.springframework.stereotype.Repository;

@Repository("jpaUserRepository")
public class JpaUserRepository implements UserRepository {
    // 구현부
}

@Repository("jdbcUserRepository")
public class JdbcUserRepository implements UserRepository {
    // 구현부
}
```
**특징**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;동일한 타입의 여러 빈 중 특정한 빈을 선택해야 할 때 사용된다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Qualifier로 특정한 이름을 명시적으로 지정해야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Spring Boot 3.4부터 ```@Qualifier```를 사용하지 않고도 @Primary를 활용하는 방법도 있다.

--------------
### @Primary – 기본적으로 선택될 빈을 지정
```@Primary```는 같은 타입의 여러 빈이 있을 때 우선적으로 선택될 빈을 지정하는 애노테이션이다.<br>
이렇게 하면 ```@Qualifier```를 사용하지 않더라도 기본적으로 어떤 빈을 주입할지 지정할 수 있다.
```java
import org.springframework.context.annotation.Primary;
import org.springframework.stereotype.Repository;

@Primary
@Repository
public class JpaUserRepository implements UserRepository {
    // 기본적으로 선택될 리포지토리 구현체
}
```
이제 UserRepository 타입의 빈이 여러 개 있더라도,<br>
```@Primary```가 붙은 ```JpaUserRepository```가 기본적으로 주입된다.
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class UserService {

    private final UserRepository userRepository;

    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
}
```
**특징**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;같은 타입의 여러 빈 중 기본적으로 선택될 빈을 설정할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Qualifier보다 더 우선적으로 적용된다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;어떤 빈이 기본적으로 사용될지를 지정하고 싶을 때 유용하다.

**@Primary vs @Qualifier**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Primary는 기본적으로 사용할 빈을 지정하는 방법이다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Qualifier는 특정한 빈을 선택해야 할 때 사용하는 방법이다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;일반적으로 @Primary를 먼저 사용하고, 특정한 빈을 선택해야 할 때 @Qualifier를 함께 사용하는 것이 좋다.

---------------
### @Component와 @ComponentScan – 빈을 자동으로 검색하고 등록
Spring Boot에서는 클래스에 ```@Component``` 애노테이션을 붙이면<br>
자동으로 Spring 컨테이너에 빈으로 등록된다.
```java
import org.springframework.stereotype.Component;

@Component
public class EmailService {
    public void sendEmail(String message) {
        System.out.println("이메일 전송: " + message);
    }
}
```
이렇게 등록된 빈은 ```@Autowired```를 사용하여 주입받을 수 있다.
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class NotificationService {

    private final EmailService emailService;

    @Autowired
    public NotificationService(EmailService emailService) {
        this.emailService = emailService;
    }

    public void notifyUser() {
        emailService.sendEmail("회원가입이 완료되었습니다.");
    }
}
```
@Component가 포함된 애노테이션 Spring Boot에서는 @Component를 포함한 여러 애노테이션이 있다.
|애노테이션|설명|
|:---|:---|
|```@Component```|기본적인 빈으로 등록하는 애노테이션|
|```@Service```|서비스 계층을 위한 @Component|
|```@Repository```|데이터 접근 계층을 위한 @Component|
|```Controller```|MVC 패턴의 컨트롤러를 위한 @Component|

이처럼 ```@Service, @Repository, @Controller```는 모두 내부적으로 ```@Component```를 포함하고 있으며,<br.
Spring이 자동으로 빈을 등록할 수 있도록 도와준다.

--------------------
### @ComponentScan – 특정 패키지를 스캔하여 빈을 자동 등록
Spring Boot는 기본적으로 ```@SpringBootApplication```이 있는 패키지를 기준으로 하위 패키지를 자동으로 스캔한다.<br>
하지만 특정 패키지만 스캔하려면 ```@ComponentScan```을 사용할 수 있다.
```java
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan(basePackages = "com.example.service")
public class AppConfig {
}
```
이렇게 하면 com.example.service 패키지 내부의 모든 @Component가 자동으로 스캔된다.

----------------
## 설정 관련 애노테이션
Spring Boot에서 설정은 애플리케이션의 동작을 정의하는 중요한 요소다.<br>
Spring은 개발자가 직접 설정 파일을 작성할 수도 있지만,<br>
애노테이션을 통해 더욱 간편하게 설정을 정의할 수 있도록 지원한다.

이번 섹션에서는 Spring Boot에서 사용되는 설정 관련 주요 애노테이션을 다룬다.

-----------------
### @Configuration – 설정 클래스를 정의하는 애노테이션
Spring Boot에서는 애플리케이션의 설정을 자바 코드 기반으로 구성할 수 있으며,<br>
이를 위한 대표적인 애노테이션이 ```@Configuration```이다.

이 애노테이션을 클래스에 추가하면 해당 클래스가 설정 클래스임을 Spring이 인식하고,<br>
해당 클래스 내에서 정의된 ```@Bean``` 메서드들을 관리한다.
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {

    @Bean(name = "exampleMessage")
    public String exampleBean() {
        return "Hello, Spring Boot!";
    }
}
```
이렇게 설정된 exampleBean은 Spring 컨테이너에 의해 관리되는 빈(Bean) 이 된다.<br>
이제 ```@Autowired```를 통해 다른 클래스에서 주입받을 수 있다.
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class ExampleService {

    private final String exampleMessage;

    @Autowired
    public ExampleService(String exampleMessage) {
        this.exampleMessage = exampleMessage;
    }

    public void printMessage() {
        System.out.println(exampleMessage);
    }
}
```
**특징**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```@Configuration```은 해당 클래스가 설정 클래스임을 명시하는 역할을 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;내부에 ```@Bean```을 사용하여 객체를 등록할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;XML 기반의 설정을 대신하여 자바 코드 기반의 설정을 가능하게 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Spring Boot에서는 자동 설정이 강력하게 동작하므로, 필요할 때만 명시적으로 사용하는 것이 좋다.

--------------
### @Bean – 수동으로 빈을 생성하고 등록
Spring Boot는 일반적으로 자동 설정(Auto Configuration)과 컴포넌트 스캔(Component Scan)을 활용하여 빈을 자동으로 등록한다.<br>
그러나, 특정 객체를 수동으로 빈으로 등록해야 할 때는 ```@Bean``` 애노테이션을 사용한다.
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class MyConfig {

    @Bean
    public EmailService emailService() {
        return new EmailService("smtp.example.com");
    }
}
```
위 코드에서 ```emailService()``` 메서드는 Spring 컨테이너에 의해 관리되는 빈으로 등록된다.
이제 해당 빈을 ```@Autowired```를 통해 주입받을 수 있다.
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class NotificationService {

    private final EmailService emailService;

    @Autowired
    public NotificationService(EmailService emailService) {
        this.emailService = emailService;
    }

    public void sendNotification(String message) {
        emailService.sendEmail(message);
    }
}
```
**특징**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Bean은 Spring 컨테이너에서 직접 관리할 객체를 수동으로 등록할 때 사용한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;XML 설정 방식의 <bean> 태그를 대체하는 역할을 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Component나 @Service와 같은 애노테이션을 붙일 수 없는 외부 라이브러리 클래스도 빈으로 등록할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Spring이 자동으로 관리하지 않는 객체를 명시적으로 설정할 때 유용하다.

-------------------
### @ComponentScan – 특정 패키지를 스캔하여 빈을 자동 등록
Spring Boot는 기본적으로 ```@SpringBootApplication```이 선언된 클래스가 위치한 패키지를 기준으로<br>
하위 패키지 내의 ```@Component, @Service, @Repository``` 등을 자동으로 스캔한다.

하지만, 특정 패키지만 스캔하고 싶을 경우 @ComponentScan을 사용하여 명시적으로 설정할 수 있다.
```java
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan(basePackages = "com.example.service")
public class AppConfig {
}
```
이렇게 설정하면 ```com.example.service``` 패키지 내부의 모든 ```@Component```가 자동으로 스캔된다.<br>
기본적으로 ```@SpringBootApplication``` 내부에 ```@ComponentScan```이 포함되어 있기 때문에,<br>
추가적으로 설정할 필요가 없지만 특정 패키지만 스캔하고 싶을 경우 유용하다.

**특징**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@ComponentScan을 사용하면 특정 패키지 내의 빈을 자동으로 검색하여 등록할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@SpringBootApplication 내부에 기본적으로 포함되어 있으므로 대부분의 경우 별도로 사용하지 않아도 된다.<br>

여러 개의 패키지를 지정할 수도 있다.<br>
```@ComponentScan(basePackages = {"com.example.service", "com.example.repository"})```<br>
특정 클래스를 기준으로 스캔을 수행할 수도 있다.<br>
```@ComponentScan(basePackageClasses = MyService.class)```

---------------------
## 환경 설정 관련 애노테이션
Spring Boot에서는 애플리케이션의 설정을 다양한 방식으로 관리할 수 있다.<br>
이를 위해 ```application.properties``` 또는 ```application.yml```과 같은 설정 파일을 사용하며,<br>
이러한 설정을 코드에서 쉽게 활용할 수 있도록 여러 환경 설정 관련 애노테이션을 제공한다.

이번 섹션에서는 Spring Boot에서 환경 설정과 관련된 주요 애노테이션을 다룬다.

-----------------
### @PropertySource – 외부 설정 파일을 로드하는 애노테이션
Spring Boot에서는 ```application.properties``` 또는 ```application.yml```을 기본 설정 파일로 사용한다.<br>
그러나, 추가적으로 다른 외부 설정 파일을 불러와야 하는 경우 ```@PropertySource```를 사용할 수 있다.

이 애노테이션을 사용하면 특정 프로퍼티 파일을 명시적으로 로드하여<br>
Spring의 환경 설정 값(Environment)에서 접근할 수 있도록 한다.
```java
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.PropertySource;
import org.springframework.beans.factory.annotation.Value;

@Configuration
@PropertySource("classpath:custom-config.properties")
public class AppConfig {

    @Value("${custom.property}")
    private String customProperty;

    public String getCustomProperty() {
        return customProperty;
    }
}
```
위 코드에서 ```@PropertySource("classpath:custom-config.properties")```는
```src/main/resources/custom-config.properties``` 파일을 로드하는 역할을 한다.

예를 들어, ```custom-config.properties``` 파일의 내용이 다음과 같다면<br>
```custom.property=Hello, PropertySource!```
해당 값을 ```@Value``` 애노테이션을 사용하여 필드에 주입할 수 있다.

**특징**<br>
```@PropertySource```는 외부 설정 파일을 추가로 불러올 때 유용하다.

파일 경로를 지정해야 하며, classpath, file, URL을 지원한다.
```
@PropertySource("file:/config/custom-config.properties")
```
@PropertySource를 통해 불러온 설정 값은 Environment 객체를 통해 조회할 수도 있다.
```java
@Autowired
private Environment env;

public void printProperty() {
    System.out.println(env.getProperty("custom.property"));
}
```

------------------
### @Value – 프로퍼티 값을 주입하는 애노테이션
Spring Boot에서는 ```@Value``` 애노테이션을 사용하여<br>
설정 파일(application.properties, application.yml)에 정의된 값을 필드에 직접 주입할 수 있다.
```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class AppConfig {

    @Value("${app.name}")
    private String appName;

    @Value("${app.version:1.0.0}") // 기본값 설정 가능
    private String appVersion;

    public void printConfig() {
        System.out.println("Application Name: " + appName);
        System.out.println("Application Version: " + appVersion);
    }
}
```
application.properties에 다음과 같은 설정이 존재할 경우:<br>
```
app.name=My Spring Boot App
```

Spring Boot는 ```@Value("${app.name}")```을 통해 해당 값을 자동으로 주입한다.<br>
또한, 설정 파일에 ```app.version```이 정의되지 않은 경우,<br>
```@Value("${app.version:1.0.0}")```에 의해 ```기본값 1.0.0```이 설정된다.

**특징**<br>
```@Value```를 사용하면 Spring 설정 값을 직접 주입받을 수 있다.<br>
기본값을 지정할 수 있어, 설정이 존재하지 않을 경우에도 안전하게 사용할 수 있다.<br>
단순한 값뿐만 아니라 배열이나 리스트에도 주입 가능하다.<br>
```java
@Value("${app.supported-languages:en,fr,de}")
private List<String> supportedLanguages;
```
SpEL(Spring Expression Language)을 사용할 수도 있다.
```java
@Value("#{systemProperties['java.version']}")
private String javaVersion;
```
-----------------
### @EnableConfigurationProperties – 프로퍼티 설정을 객체로 매핑
Spring Boot에서는 ```@EnableConfigurationProperties``` 애노테이션을 사용하여<br>
설정 파일(application.properties, application.yml)의 값을 객체에 매핑할 수 있다.

이 방식은 ```@Value```보다 더 구조적인 방식으로 설정 값을 관리할 수 있도록 한다.
```java
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.context.annotation.Configuration;

@Configuration
@ConfigurationProperties(prefix = "app")
public class AppConfig {

    private String name;
    private String version;

    // Getter 및 Setter
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getVersion() {
        return version;
    }

    public void setVersion(String version) {
        this.version = version;
    }
}
```
이제 application.yml에서 설정 값을 다음과 같이 정의할 수 있다.
```
app:
  name: My Spring Boot App
  version: 2.0.0
```
그리고 @Autowired를 통해 해당 객체를 주입받아 사용할 수 있다.
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class AppService {

    private final AppConfig appConfig;

    @Autowired
    public AppService(AppConfig appConfig) {
        this.appConfig = appConfig;
    }

    public void printAppInfo() {
        System.out.println("Application Name: " + appConfig.getName());
        System.out.println("Application Version: " + appConfig.getVersion());
    }
}
```
**특징**<br>
@EnableConfigurationProperties와 @ConfigurationProperties를 사용하면<br>
설정 값을 하나의 객체로 묶어서 관리할 수 있다.

객체 내의 필드 이름과 설정 파일의 키(prefix 포함)가 일치해야 한다.

기본적으로 ```@ConfigurationProperties```는 Setter 기반 바인딩을 사용하지만,<br>
```@ConstructorBinding```을 사용하면 생성자 기반 바인딩도 가능하다.
```java
@ConfigurationProperties(prefix = "app")
@ConstructorBinding
public class AppConfig {
    private final String name;
    private final String version;

    public AppConfig(String name, String version) {
        this.name = name;
        this.version = version;
    }
}
```
-----------------
## 트랜잭션 관리 애노테이션
Spring Boot에서 트랜잭션(Transaction)은 데이터의 일관성과 무결성을 보장하는 중요한 개념이다.<br>
특히, 데이터베이스를 다루는 애플리케이션에서는 트랜잭션을 적절히 활용하지 않으면<br>
데이터가 불완전하게 저장되거나 예상치 못한 오류가 발생할 수 있다.

Spring은 이러한 트랜잭션을 효과적으로 관리할 수 있도록<br>
```@Transactional``` 애노테이션을 제공하며, 이를 통해 데이터베이스 작업을 안정적으로 수행할 수 있다.

이 섹션에서는 Spring Boot에서 트랜잭션을 관리하는 ```@Transactional``` 애노테이션의 개념과 사용법을 상세히 다룬다.

------------
### @Transactional – 트랜잭션을 관리하는 핵심 애노테이션
Spring Boot에서 트랜잭션을 적용할 때 가장 기본적으로 사용하는 것이 @Transactional 애노테이션이다.<br>
이 애노테이션을 활용하면 특정 메서드 또는 클래스의 데이터 변경 작업을 하나의 트랜잭션 단위로 묶을 수 있다.

즉, 해당 메서드에서 예외가 발생하면 자동으로 롤백(Rollback) 되어 데이터의 무결성을 유지할 수 있다.
```java
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

@Service
public class UserService {

    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    @Transactional
    public void registerUser(User user) {
        userRepository.save(user);
        sendWelcomeEmail(user); // 이 메서드에서 예외 발생 시 전체 롤백
    }

    private void sendWelcomeEmail(User user) {
        throw new RuntimeException("이메일 전송 실패"); // 예외 발생
    }
}
```
위 코드에서 ```registerUser``` 메서드에 ```@Transactional```이 적용되어 있기 때문에,
```sendWelcomeEmail``` 메서드에서 예외가 발생하면 이전의 ```userRepository.save(user)```도 롤백된다.
즉, 데이터베이스에는 아무런 변경 사항이 반영되지 않는다.

**@Transactional의 특징**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Transactional이 적용된 메서드에서 예외가 발생하면 자동으로 롤백된다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;읽기 전용(read-only) 트랜잭션을 설정할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;트랜잭션 전파 옵션(Propagation)과 격리 수준(Isolation Level)을 설정할 수 있다.

-------------
### 트랜잭션의 기본 동작 방식
Spring Boot에서 @Transactional이 적용된 메서드는<br>
다음과 같은 방식으로 트랜잭션이 시작되고 종료된다.

메서드 실행 전: 트랜잭션이 시작됨<br>
메서드 실행 중:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;정상적으로 실행되면, 트랜잭션이 커밋(Commit)됨<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예외가 발생하면, 트랜잭션이 롤백(Rollback)됨<br>
메서드 실행 후: 트랜잭션 종료

Spring Boot에서 ```@Transactional```은 기본적으로 "런타임 예외(RuntimeException)"가 발생해야만 롤백된다.<br>
즉,``` NullPointerException, IllegalArgumentException``` 같은 예외가 발생하면 롤백이 되지만,<br>
```Checked Exception(예: IOException, SQLException)```은 기본적으로 롤백되지 않는다.

```java
@Transactional
public void updateUser(User user) throws IOException {
    userRepository.save(user);
    throw new IOException("파일 저장 실패"); // Checked Exception → 롤백되지 않음
}
```
위 코드에서 IOException은 Checked Exception이므로, 기본적으로 롤백되지 않는다.

**Checked Exception도 롤백되게 하려면?** <br>
만약 Checked Exception도 롤백되도록 설정하려면 ```rollbackFor``` 옵션을 추가해야 한다.
```java
@Transactional(rollbackFor = IOException.class)
public void updateUser(User user) throws IOException {
    userRepository.save(user);
    throw new IOException("파일 저장 실패"); // 롤백됨
}
```
### @Transactional의 주요 옵션
@Transactional은 다양한 옵션을 지원하여 트랜잭션의 동작을 세밀하게 조정할 수 있다.<br>
가장 중요한 옵션들은 다음과 같다.

|옵션|설명|
|:---|:---|
|propagation|트랜잭션 전파 방식을 설정|
|isolation|트랜잭션의 격리 수준을 설정|
|readOnly|읽기 전용 트랜잭션 여부 설정|
|rollbackFor|롤백할 예외 타입 지정|
|noRollbackFor|롤백하지 않을 예외 타입 지정|

---------------
### @Transactional의 주요 사용 예제
다양한 옵션을 조합하여 트랜잭션을 설정할 수 있다.

(1) 읽기 전용 트랜잭션 (readOnly = true) 읽기 전용 트랜잭션을 설정하면 데이터를 변경하는 작업이 방지되며,<br>
성능 최적화가 가능하다.
```java
@Transactional(readOnly = true)
public User getUser(Long id) {
    return userRepository.findById(id).orElse(null);
}
```
위 코드에서는 데이터를 조회하는 메서드에 @Transactional(readOnly = true) 를 설정하여<br>
불필요한 트랜잭션 오버헤드를 줄일 수 있다.

(2) 특정 예외 발생 시 롤백 (rollbackFor) 기본적으로 Checked Exception은 롤백되지 않지만, rollbackFor을 사용하여 롤백 가능하다.
```java
@Transactional(rollbackFor = Exception.class)
public void processOrder(Order order) throws Exception {
    orderRepository.save(order);
    throw new Exception("주문 처리 실패"); // 롤백됨
}
```
(3) 특정 예외 발생 시 롤백 방지 (noRollbackFor) 반대로, 특정 예외가 발생하더라도 롤백되지 않도록 설정할 수도 있다.
```java
@Transactional(noRollbackFor = IllegalArgumentException.class)
public void updateUserProfile(User user) {
    userRepository.save(user);
    throw new IllegalArgumentException("잘못된 사용자 정보");
}
```
위 코드에서는 IllegalArgumentException이 발생해도 트랜잭션이 커밋(Commit)됨<br>
즉, userRepository.save(user)는 유지된다.

------------
## @Async – 비동기 작업을 수행하는 애노테이션
일반적으로 **Spring Boot의 메서드는 동기(Synchronous)적** 으로 실행된다.<br>
즉, 한 메서드가 실행을 완료해야 다음 코드가 실행된다.

그러나 네트워크 호출, 파일 입출력, 대용량 데이터 처리와 같은 시간이 오래 걸리는 작업을 동기적으로 실행하면 애플리케이션 성능이 저하될 수 있다.<br>
이 문제를 해결하기 위해 Spring Boot에서는 @Async를 사용하여 비동기 처리를 할 수 있다.

----------------
### @Async의 기본 사용법
Spring Boot에서 ```@Async```를 적용하면 해당 메서드는 별도의 스레드에서 실행된다.<br>
즉, 호출한 메서드는 즉시 반환되며, 작업은 백그라운드에서 실행된다.

1. 비동기 메서드 실행
```java
import org.springframework.scheduling.annotation.Async;
import org.springframework.stereotype.Service;

@Service
public class AsyncService {

    @Async
    public void executeAsyncTask() {
        System.out.println("비동기 작업 시작: " + Thread.currentThread().getName());
        try {
            Thread.sleep(3000); // 3초 동안 대기
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
        System.out.println("비동기 작업 완료: " + Thread.currentThread().getName());
    }
}
```
위 코드를 실행하면 ```executeAsyncTask()```가 호출된 후 즉시 반환되며,<br>
백그라운드에서 별도의 스레드가 할당되어 3초 동안 실행된다.

2. 비동기 메서드 실행 예제
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class AsyncController {

    @Autowired
    private AsyncService asyncService;

    @GetMapping("/async-task")
    public String runAsyncTask() {
        System.out.println("요청 처리 스레드: " + Thread.currentThread().getName());
        asyncService.executeAsyncTask();
        return "비동기 작업 실행됨!";
    }
}
```
이제 ```http://localhost:8080/async-task```로 요청하면,<br>
컨트롤러는 즉시 응답을 반환하지만, 실제 작업은 백그라운드에서 실행된다.

출력 예시:
```
요청 처리 스레드: http-nio-8080-exec-1
비동기 작업 시작: taskExecutor-1
비동기 작업 완료: taskExecutor-1
```
위 로그를 보면, 요청을 처리하는 스레드와 비동기 작업을 실행하는 스레드가 서로 다르다는 것을 알 수 있다.

-------------
### @Async 사용 시 주의사항
@Async를 올바르게 사용하려면 몇 가지 중요한 사항을 이해해야 한다.

① @EnableAsync를 반드시 설정해야 한다
Spring Boot에서 @Async를 사용하려면 비동기 처리를 활성화해야 한다.
이를 위해 @EnableAsync 애노테이션을 설정 클래스에 추가해야 한다.

import org.springframework.context.annotation.Configuration;
import org.springframework.scheduling.annotation.EnableAsync;

@Configuration
@EnableAsync
public class AsyncConfig {
}
만약 @EnableAsync를 추가하지 않으면 @Async가 동작하지 않고 동기적으로 실행된다.


