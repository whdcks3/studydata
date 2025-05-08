# 1. RESTful API의 고급 설계 원칙
## 1-1. RESTful API 설계 개요
### RESTful API란 무엇인가?
RESTful API는 **REST(Representational State Transfer)** 원칙을 따르는 API 설계 방식이다.<br>
REST는 웹의 설계 원칙을 기반으로 한 소프트웨어 아키텍처 스타일이며, 자원을 중심으로 한 구조를 따른다.<br>
RESTful API는 웹 서비스에서 데이터를 주고받기 위해 널리 사용되며, HTTP 프로토콜을 활용하여 리소스에 대한 CRUD(Create, Read, Update, Delete) 작업을 수행하는 것이 일반적이다.

RESTful API의 핵심 개념은 리소스(Resource) 기반 설계이다.<br>
RESTful API에서는 클라이언트가 서버의 특정 리소스를 식별하고, 이를 조작하는 방식으로 데이터를 처리한다.<br>
이 과정에서 HTTP 메서드가 리소스에 대한 행동을 나타내며, URL이 리소스를 식별하는 역할을 한다.

예를 들어, 사용자의 정보를 조회하는 RESTful API의 엔드포인트는 다음과 같이 정의할 수 있다.
```
GET /users/{id}
```
이 API는 ```{id}```에 해당하는 사용자의 정보를 반환하며, ```users```는 리소스의 집합을 의미한다. RESTful API는 명확하고 직관적인 구조를 가지므로, 개발자들이 쉽게 이해하고 사용할 수 있다는 장점이 있다.

------------------
### RESTful API의 특징
RESTful API를 설계할 때는 REST 아키텍처의 주요 원칙을 준수해야 한다. RESTful API의 특징을 이해하는 것은 효과적인 API 설계를 위한 필수적인 과정이다.

**클라이언트-서버 구조(Client-Server Architecture)**<br>
RESTful API는 클라이언트와 서버 간의 명확한 역할 분리를 기반으로 한다.<br>
클라이언트는 사용자 인터페이스를 담당하며, 서버는 데이터를 처리하고 저장하는 역할을 한다.<br>
이러한 구조는 시스템의 확장성을 높이며, 클라이언트와 서버가 독립적으로 개발될 수 있도록 한다.

예를 들어, 웹 브라우저에서 사용자가 특정 상품을 조회하면, 클라이언트는 RESTful API를 통해 서버에서 데이터를 가져와 화면에 표시하는 방식으로 동작한다.
```
GET /products/{id}
```
위 요청을 통해 서버는 id에 해당하는 상품 데이터를 반환하고, 클라이언트는 이를 UI에 표시한다.<b>
이 과정에서 클라이언트는 데이터 저장이나 비즈니스 로직을 처리하지 않으며, 서버는 UI에 대해 알 필요가 없다.

**무상태(Stateless) 원칙**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;RESTful API는 무상태(Stateless) 원칙을 따른다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;이는 서버가 클라이언트의 이전 요청 상태를 저장하지 않는다는 것을 의미한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;모든 요청은 독립적으로 처리되며, 필요한 모든 정보는 요청에 포함되어야 한다.

예를 들어, 사용자가 서버에 요청을 보낼 때, 서버는 해당 사용자의 세션 상태를 유지하지 않는다.<br>
대신, 클라이언트는 매 요청마다 필요한 인증 정보를 포함하여 서버가 요청을 인증할 수 있도록 해야 한다.
```
GET /users/profile
Authorization: Bearer <JWT_TOKEN>
```
위 요청에서는 Authorization 헤더에 JWT(Json Web Token) 토큰을 포함하여 사용자를 인증한다.<br>
서버는 클라이언트의 로그인 상태를 기억하지 않으며, 매 요청을 개별적으로 처리한다.

------------------
**캐시 가능(Cacheable) 설계**<br>
RESTful API는 클라이언트가 응답을 캐싱할 수 있도록 설계되어야 한다.<br>
이를 통해 불필요한 네트워크 요청을 줄이고, 성능을 최적화할 수 있다.

캐싱을 적용하기 위해 HTTP의 Cache-Control 헤더를 활용할 수 있다.
```
Cache-Control: max-age=3600, public
```
위 설정은 클라이언트가 1시간(3600초) 동안 캐시된 응답을 사용할 수 있도록 지정하는 것이다.<br>
이를 통해 동일한 데이터를 반복적으로 요청하는 경우 서버의 부하를 줄일 수 있다.

**계층화된 시스템(Layered System)**<br>
RESTful API는 계층화된 구조를 가질 수 있다.<br>
즉, 클라이언트의 요청이 여러 계층을 거쳐 처리될 수 있으며, 클라이언트는 이러한 내부 구조를 알 필요가 없다.

예를 들어, 클라이언트는 직접 데이터베이스에 접근하지 않고, API 게이트웨이나 프록시 서버를 통해 요청을 처리할 수도 있다.<br>
이러한 계층 구조는 보안과 성능 향상에 기여하며, 로드 밸런서 등을 추가하여 트래픽을 효율적으로 관리할 수 있도록 한다.

**일관된 인터페이스(Uniform Interface)**<br>
RESTful API는 일관된 인터페이스를 제공해야 한다.<br>
즉, API의 사용 방식이 일관되게 유지되어야 하며, 리소스 경로와 HTTP 메서드의 조합이 예측 가능해야 한다.

예를 들어, 다음과 같이 API를 설계하면 일관성을 유지할 수 있다.
```
GET /products         # 모든 상품 조회
GET /products/{id}    # 특정 상품 조회
POST /products        # 새로운 상품 추가
PUT /products/{id}    # 기존 상품 정보 수정
DELETE /products/{id} # 상품 삭제
```
위처럼 API가 일관된 패턴을 가지면 클라이언트가 API를 예측하기 쉬워지고, 문서화 없이도 직관적으로 이해할 수 있다.

------------------
### RESTful API 설계 시 고려해야 할 사항
RESTful API를 설계할 때는 다음과 같은 사항을 고려해야 한다.

**일관성 유지**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;엔드포인트 경로(/users, /orders 등)가 일관성을 유지해야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;응답 형식이 일관되게 유지되어야 한다.

**리소스 중심 설계**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;API는 동작이 아니라 리소스를 중심으로 설계되어야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, /getUser 대신 /users/{id}로 설계하는 것이 RESTful 방식이다.

**HTTP 메서드의 올바른 사용**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;API의 동작을 HTTP 메서드(GET, POST, PUT, DELETE)와 매핑해야 한다.

**URI 네이밍 컨벤션**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URI는 짧고 직관적으로 작성되어야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;/users vs. /userList → /users가 RESTful 방식이다.

**요청 및 응답의 표준화**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JSON 또는 XML을 사용하여 일관된 응답 구조를 제공해야 한다.

**확장성 고려**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;API의 확장성을 고려하여 새로운 기능을 추가할 때 기존 API가 깨지지 않도록 해야 한다.

-----------------
### RESTful API와 SOAP API의 차이점
RESTful API는 SOAP(Simple Object Access Protocol) API와 비교하여 더 가볍고 직관적인 설계를 제공한다.

비교 항목|RESTful API|SOAP API
:---|:---|:---
프로토콜|HTTP 기반|HTTP, SMTP 등 다양한 프로토콜 지원
데이터 형식|JSON, XML 등 다양함|XML
상태 관리|무상태(Stateless)|상태를 유지할 수 있음
사용 용도|웹 및 모바일 API, 마이크로서비스|엔터프라이즈 애플리케이션, 보안이 중요한 서비스

RESTful API는 보다 유연하고 확장성이 뛰어나기 때문에, 웹과 모바일 애플리케이션에서 가장 널리 사용되는 방식이다.

---------------------
## 1-2. 리소스 설계 원칙
### 리소스란 무엇인가?
RESTful API에서 리소스(Resource) 는 서버가 관리하는 데이터의 단위를 의미한다.<br>
API를 통해 접근하고 조작할 수 있는 대상이 모두 리소스가 될 수 있으며,<br>
예를 들어 사용자(User), 주문(Order), 제품(Product) 등이 이에 해당한다.

리소스는 API에서 **고유한 URI(Uniform Resource Identifier)** 를 통해 식별된다.<br>
API 사용자는 특정 리소스를 조회, 추가, 수정 또는 삭제하기 위해 정확한 URI를 사용해야 한다.

예를 들어, 특정 사용자의 정보를 조회하는 엔드포인트를 다음과 같이 정의할 수 있다.
```
GET /users/{userId}
```
위 URI는 userId에 해당하는 특정 사용자의 정보를 조회하는 API 엔드포인트이다.

---------------
### RESTful한 리소스 설계의 원칙
RESTful API에서 리소스를 설계할 때는 다음 원칙을 따라야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;명사 기반의 리소스 경로 사용<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;일관된 URI 패턴 유지<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;계층적 구조 활용<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;HTTP 메서드와 리소스의 관계 명확화<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;복수형 사용 권장<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;행위(Verb) 대신 리소스를 중심으로 설계

이제 각 원칙에 대해 자세히 살펴보자.

----------------------
### 명사 기반의 리소스 경로 사용
RESTful API의 URI는 리소스를 표현해야 한다.<br>
즉, 명사(Noun) 기반으로 설계 해야 하며, 동사(Verb)를 포함하지 않아야 한다.

잘못된 예시:
```
GET /getUser
POST /createOrder
DELETE /removeProduct
```
올바른 예시:
```
GET /users/{userId}
POST /orders
DELETE /products/{productId}
```
잘못된 예시에서는 API 경로에 동사(getUser, createOrder) 가 포함되어 있다.<br>
RESTful API에서는 URI가 리소스를 표현하는 역할 을 해야 하므로,<br>
HTTP 메서드(GET, POST, DELETE) 자체가 수행할 동작을 나타내도록 설계해야 한다.

즉, API는 GET 요청이면 데이터를 조회하고, POST 요청이면 데이터를 생성하는 등 HTTP 메서드에 따라 동작을 정의 해야 한다.

---------------------
### 일관된 URI 패턴 유지
API의 URI 설계는 **일관된 패턴을 유지해야 한다.**<br>
API를 사용하는 개발자가 직관적으로 이해할 수 있도록 일반적인 RESTful 설계 패턴을 따르는 것이 중요하다.

다음과 같은 URI 패턴을 유지하는 것이 좋다.

올바른 예시:
```
GET /users/{userId}/orders  # 특정 사용자의 주문 목록 조회
POST /users/{userId}/orders # 특정 사용자에 대한 주문 생성
GET /products/{productId}   # 특정 제품 정보 조회
```
위 예제에서 ```/users/{userId}/orders``` 패턴은 특정 사용자와 관련된 주문을 의미한다.<br>
즉, 계층적 구조를 반영하여 API URI의 의미가 명확하도록 설계 하는 것이 중요하다.

---------------------
### 계층적 구조 활용
RESTful API의 URI는 리소스 간의 계층 구조를 반영 해야 한다.<br>
예를 들어, 사용자가 작성한 댓글 데이터를 조회하는 API를 설계할 경우,<br>
댓글(comments)이 사용자(users)에 속한다는 점을 반영하여 다음과 같이 설계할 수 있다.

올바른 예시:
```
GET /users/{userId}/comments
```
이처럼 계층적 관계를 표현하면 API의 가독성과 직관성이 향상된다.<br>
하지만 모든 관계를 계층 구조로 표현하는 것은 바람직하지 않다.<Br>
계층 구조가 너무 깊어지면 API 사용성이 낮아질 수 있기 때문이다.

잘못된 예시 (과도한 계층화):
```
GET /users/{userId}/orders/{orderId}/items/{itemId}/details
```
이처럼 너무 깊은 계층 구조 는 API 사용성을 떨어뜨릴 수 있다.<br>
이런 경우에는 필요한 정보를 쿼리 파라미터로 전달하는 방식 도 고려할 수 있다.

개선된 예시:
```
GET /orders/{orderId}/items?details=true
```
이처럼 계층적 구조를 유지하되 불필요한 중첩을 피하는 것이 중요하다.

---------------------
### HTTP 메서드와 리소스의 관계 명확화
RESTful API에서는 HTTP 메서드와 리소스의 관계를 명확하게 정의 해야 한다.<br>
즉, HTTP 메서드가 수행하는 동작이 API의 의미와 일관성을 가져야 한다.

HTTP 메서드|동작(의미)|예제 URI
:---|:---|:---
GET|리소스 조회|/users/{userId}
POST|리소스 생성|/users
PUT|리소스 전체 수정|/users/{userId}
PATCH|리소스 부분 수정|/users/{userId}
DELETE|리소스 삭제|/users/{userId}

예를 들어, 사용자의 정보를 수정하는 API를 설계할 때는 다음과 같이 정의할 수 있다.

올바른 예시:
```
PUT /users/{userId}   # 사용자 정보 전체 수정
PATCH /users/{userId} # 사용자 정보 일부 수정
```
잘못된 예시:
```
POST /users/update
GET /users/update/{userId}
```
잘못된 예시에서는 POST /users/update 와 같은 동사(update)가 포함되어 있다.<br>
RESTful API에서는 HTTP 메서드 자체가 동작을 나타내므로, 동사를 포함하지 않는 것이 원칙 이다.

-------------------
### 복수형 사용 권장
RESTful API에서는 리소스 이름을 복수형으로 표현하는 것이 권장된다.<br>
이유는 하나의 리소스가 단일 객체가 아니라, 동일한 유형의 리소스 집합을 나타내기 때문이다.

올바른 예시:
```
GET /users
GET /products
```
잘못된 예시:
```
GET /user
GET /product
```
복수형을 사용하면 API가 보다 **직관적으로 설계** 될 수 있으며,<br>
특정 리소스 하나만 조회할 때는 /{id} 를 추가하여 구별할 수 있다.

예제:
```
GET /users          # 모든 사용자 조회
GET /users/{userId} # 특정 사용자 조회
```
이처럼 복수형을 사용하면 API 사용자가 **리소스의 개념을 더 쉽게 이해** 할 수 있다.

-----------------
### 행위(Verb) 대신 리소스를 중심으로 설계
RESTful API는 행위(Verb)가 아닌 리소스(Resource)를 중심으로 설계 되어야 한다.<br>
즉, GET, POST, PUT, DELETE 와 같은 HTTP 메서드를 활용하여 리소스를 조작하는 방식으로 API를 설계해야 한다.

잘못된 예시:
```
GET /getUserOrders
POST /addNewProduct
DELETE /removeUserAccount
```
올바른 예시:
```
GET /users/{userId}/orders
POST /products
DELETE /users/{userId}
```
잘못된 예시에서는 URI에 get, add, remove 와 같은 동사가 포함되어 있다.<br>
올바른 설계 방식은 리소스 중심으로 URI를 정의하고, 동작은 HTTP 메서드로 표현하는 것 이다.

----------------------------
## 1-3. 상태 전이와 API 설계
### 상태 전이(State Transition)란 무엇인가?
RESTful API에서 상태 전이(State Transition) 는 클라이언트가 API 요청을 보낼 때 리소스의 상태가 변경되는 과정을 의미한다.<br>
즉, 사용자의 특정 액션이 API를 통해 서버로 전달되면서 리소스의 상태가 변할 수 있다.

이 개념은 웹 애플리케이션이 특정 동작을 수행할 때 현재 상태를 기반으로 변화하는 과정 을 의미하며, HTTP 요청을 통해 이루어진다.

예를 들어, 사용자가 주문을 생성하고, 결제하고, 배송 상태를 변경하는 과정을 생각해보자.<br>
각 단계에서 API 호출을 통해 주문의 상태가 변할 수 있다.

**주문 생성**: POST /orders (상태: "주문 접수")<br>
**결제 완료**: PATCH /orders/{orderId} (상태: "결제 완료")<br>
**배송 시작**: PATCH /orders/{orderId} (상태: "배송 중")<br>
**배송 완료**: PATCH /orders/{orderId} (상태: "배송 완료")<br>
이처럼 API를 통해 리소스의 상태가 전이되며, 이 상태 전이가 RESTful 설계에서 중요한 개념 이다.

----------------------
### 상태 전이와 엔드포인트 설계
API를 설계할 때 상태 전이를 어떻게 처리할 것인지 명확한 기준을 세워야 한다.<br>
이때 다음과 같은 설계 방식을 고려할 수 있다.

**리소스 중심의 상태 전이**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;상태가 변하는 리소스를 기준으로 API를 설계한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;상태 값은 API의 응답(JSON 등)에 포함될 수 있다.<br>

**HTTP 메서드를 활용한 상태 전이**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```GET```: 리소스 조회 (상태 변화 없음)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```POST```: 새로운 리소스 생성 (새로운 상태로 진입)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```PUT```: 기존 리소스의 상태를 완전히 변경<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```PATCH```: 특정 필드 또는 일부 상태만 변경<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```DELETE```: 리소스를 제거하여 상태를 종료

**명확한 상태 변경을 위한 API 패턴**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;특정 상태로 변경하는 API를 따로 제공할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, 주문 상태를 변경하는 API를 PATCH 요청으로 관리한다.

예제:
```
PATCH /orders/{orderId}/status
```
이 API를 호출할 때 요청 본문(JSON)에서 새로운 상태 값을 전달할 수 있다.
```
{
  "status": "배송 완료"
}
```
이 방식은 클라이언트가 명확하게 상태를 지정하여 전이하도록 유도 할 수 있다.

------------------
### 상태 전이 방식의 예제
이제 상태 전이를 어떻게 API에서 구현하는지 간단한 코드 예제를 살펴보자.<br>
아래 코드는 주문 상태를 변경하는 RESTful API의 예제이다.
```java
@RestController
@RequestMapping("/orders")
public class OrderController {

    @PatchMapping("/{orderId}/status")
    public ResponseEntity<Order> updateOrderStatus(@PathVariable Long orderId, @RequestBody OrderStatusUpdateRequest request) {
        Order order = orderService.findById(orderId);
        
        if (order == null) {
            return ResponseEntity.notFound().build();
        }

        // 상태 업데이트 로직
        order.setStatus(request.getStatus());
        orderService.save(order);

        return ResponseEntity.ok(order);
    }
}
```
위 코드에서는 ```PATCH /orders/{orderId}/status``` 엔드포인트를 사용하여 주문의 상태를 변경할 수 있다.<br>
요청 본문(JSON)에서 새로운 상태 값을 전달하면 서버에서 해당 주문의 상태를 업데이트한다.

----------------
### 상태 전이 시 고려해야 할 사항
**비즈니스 로직을 반영한 상태 전이**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;상태 변경이 올바르게 이루어져야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, "배송 완료" 상태로 변경하기 전에 반드시 "배송 중" 상태를 거쳐야 하는 경우가 있다.

**유효한 상태 값만 허용**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트가 존재하지 않는 상태 값으로 변경하지 못하도록 해야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, OrderStatus enum을 정의하여 허용된 상태만 설정할 수 있도록 한다.
```
public enum OrderStatus {
    PENDING,      // 주문 접수
    PAID,         // 결제 완료
    SHIPPED,      // 배송 중
    DELIVERED,    // 배송 완료
    CANCELED      // 주문 취소
}
```
이렇게 하면 클라이언트가 잘못된 상태 값을 전달하는 것을 방지할 수 있다.

**상태 변경에 대한 권한 검증**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;특정 사용자가 특정 상태로 변경할 수 있는지 확인해야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, "배송 완료" 상태는 관리자만 변경할 수 있도록 설정할 수 있다.<br>
```java
if (!currentUser.isAdmin()) {
    return ResponseEntity.status(HttpStatus.FORBIDDEN).build();
}
```

**상태 전이 로깅**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;상태 변경 이력을 남기는 것이 중요하다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, 주문이 "결제 완료" 상태로 변경되었을 때, 로그를 남길 수 있다.
```
log.info("Order {} status changed to {}", orderId, request.getStatus());
```

-------------
### 상태 전이를 고려한 API 설계의 중요성
API에서 상태 전이는 단순한 CRUD(Create, Read, Update, Delete) 설계보다 더 복잡한 문제를 포함한다.<br>
리소스의 상태가 변화하는 과정에서 비즈니스 로직이 포함될 가능성이 높으며,<br>
이를 잘못 설계하면 **불필요한 API 호출 증가, 데이터 일관성 문제, 보안 취약점** 등이 발생할 수 있다.

따라서 상태 전이를 설계할 때는 다음과 같은 점을 고려해야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**명확한 상태 정의** - 리소스가 가질 수 있는 상태를 미리 정의하고 API에서 일관성 있게 적용해야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**비즈니스 규칙 반영** - 상태 전이 간의 유효성을 검증하는 로직이 필요하다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**HTTP 메서드와 URI 설계** - PATCH 또는 PUT을 활용하여 상태 변경을 구현해야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**상태 변경 로그 및 검증** - 변경된 상태를 추적하고, 변경 가능한 사용자를 제한할 필요가 있다.

이러한 원칙을 적용하면 RESTful API에서 상태 전이를 보다 안정적으로 관리 할 수 있으며,<br>
클라이언트와 서버 간의 API 사용 경험을 더욱 향상시킬 수 있다.

-----------------
# 2. RESTful API에서 HTTP 상태 코드 활용
## 2-1. HTTP 상태 코드 개요
### HTTP 상태 코드란?
HTTP 상태 코드는 클라이언트가 서버에 요청을 보냈을 때, **서버가 해당 요청을 어떻게 처리했는지** 를 응답하는 표준 코드이다.<br>
RESTful API에서 올바른 상태 코드를 사용하는 것은 **API의 신뢰성과 사용성을 높이는 핵심 요소** 이다.

이 상태 코드는 숫자 3자리 로 구성되며, 첫 번째 숫자에 따라 응답의 의미가 달라진다.

예를 들어, 다음과 같은 의미를 가진다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```2xx```: 요청이 정상적으로 처리됨 (성공)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```3xx```: 클라이언트가 추가적인 조치를 해야 함 (리다이렉션)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```4xx```: 클라이언트의 잘못된 요청 (클라이언트 오류)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```5xx```: 서버에서 요청을 정상적으로 처리하지 못함 (서버 오류)

---------------
### HTTP 상태 코드의 필요성
RESTful API에서 올바른 상태 코드를 반환하는 것은 단순히 응답을 전달하는 것 이상의 의미를 가진다.

**API의 신뢰성을 높임**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;올바른 상태 코드가 없으면, 클라이언트는 서버의 응답을 해석하는 데 어려움을 겪을 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, 실패한 요청에 대해 200 OK 를 반환하면 클라이언트는 성공으로 오인할 수 있다.

**디버깅과 유지보수를 용이하게 함**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;적절한 상태 코드가 제공되면, 클라이언트와 서버 개발자는 API의 동작을 쉽게 파악할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, 404 Not Found 가 반환되면, 클라이언트는 해당 리소스가 존재하지 않음을 즉시 알 수 있다.

**HTTP 프로토콜의 원칙을 따름**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;RESTful API는 HTTP 프로토콜을 기반으로 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;따라서 올바른 상태 코드를 사용하는 것은 REST 아키텍처 스타일을 준수하는 필수 요소 이다.

--------------------
### 상태 코드의 주요 카테고리
HTTP 상태 코드는 크게 다섯 개의 범주로 나뉜다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```1xx (정보)``` : 클라이언트의 요청을 처리 중임을 의미<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```2xx (성공)``` : 요청이 정상적으로 처리됨<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```3xx (리다이렉션)``` : 요청을 완료하려면 추가 동작이 필요<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```4xx (클라이언트 오류)``` : 클라이언트 측에서 문제가 발생<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```5xx (서버 오류)``` : 서버에서 요청을 정상적으로 처리하지 못함

이 중 RESTful API에서는 2xx, 4xx, 5xx 상태 코드가 가장 중요하게 사용된다.

----------------
### 2xx (성공) 상태 코드
서버가 클라이언트의 요청을 정상적으로 처리했음을 의미하는 코드이다.

**200 OK**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;가장 일반적인 성공 응답 코드.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GET, PUT, PATCH, DELETE 요청이 성공했을 때 사용된다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;응답 본문에 데이터를 포함할 수 있다.

**201 Created**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;새로운 리소스가 성공적으로 생성되었을 때 사용한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;보통 POST 요청에서 사용된다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;응답 헤더에 Location 을 포함하여 생성된 리소스의 URI를 제공할 수 있다.

**204 No Content**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;요청은 성공적으로 처리되었지만, 응답 본문을 반환할 필요가 없을 때 사용된다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;보통 DELETE 요청에서 사용된다.

예제:
```java
@PostMapping("/users")
public ResponseEntity<User> createUser(@RequestBody User user) {
    User savedUser = userService.save(user);
    return ResponseEntity.status(HttpStatus.CREATED).body(savedUser);
}
```
------------------
### 4xx (클라이언트 오류) 상태 코드
클라이언트가 잘못된 요청을 보냈을 때 사용된다.

**400 Bad Request**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;요청이 잘못되었거나, 유효성 검사를 통과하지 못한 경우.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, 필수 입력값이 누락된 경우 사용된다.

**401 Unauthorized**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트가 인증되지 않았을 때 사용된다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;보통 API에서 인증 토큰이 누락되었거나, 올바르지 않을 때 발생한다.

**403 Forbidden**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트가 해당 리소스에 접근할 권한이 없을 때 사용된다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, 관리자 권한이 없는 사용자가 특정 API를 호출할 때 발생할 수 있다.

**404 Not Found**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;요청한 리소스가 존재하지 않을 때 사용된다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트가 잘못된 엔드포인트를 호출했거나, 데이터가 존재하지 않는 경우 발생할 수 있다.

예제:
```java
@GetMapping("/users/{id}")
public ResponseEntity<User> getUser(@PathVariable Long id) {
    User user = userService.findById(id);
    
    if (user == null) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).build();
    }

    return ResponseEntity.ok(user);
}
```
---------------
### 5xx (서버 오류) 상태 코드
서버에서 요청을 정상적으로 처리하지 못할 때 사용된다.

**500 Internal Server Error**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;서버에서 예상치 못한 오류가 발생했을 때 사용된다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;일반적으로 예외가 발생하거나, 내부 오류가 있는 경우 발생할 수 있다.

**502 Bad Gateway**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;서버가 다른 서버로부터 잘못된 응답을 받았을 때 사용된다.<br>

**503 Service Unavailable**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;서버가 현재 요청을 처리할 수 없을 때 사용된다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;과부하 상태이거나, 유지보수 중일 때 발생할 수 있다.

예제:
```java
@ExceptionHandler(Exception.class)
public ResponseEntity<String> handleGlobalException(Exception ex) {
    return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
                         .body("서버 내부 오류 발생");
}
```
-------------------------
### HTTP 상태 코드의 활용
올바른 상태 코드를 사용하면 API의 가독성과 신뢰성이 높아진다.<br>
API 응답이 일관되게 동작하도록 설계하고, 클라이언트가 이를 해석할 수 있도록 명확한 기준을 설정해야 한다.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```200 OK```: GET 요청의 일반적인 성공 응답<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```201 Created```: 새로운 리소스 생성 시<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```204 No Content```: 응답 본문이 필요 없는 경우<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```400 Bad Request```: 요청이 잘못된 경우<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```401 Unauthorized```: 인증 실패<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```403 Forbidden```: 권한 부족<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```404 Not Found```: 리소스 없음<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```500 Internal Server Error```: 서버 내부 오류

이러한 원칙을 지키면 RESTful API의 신뢰성을 높이고, 클라이언트와의 소통을 원활하게 할 수 있다.

-------------------------
## 2-2. 상태 코드별 활용 사례
### 상태 코드의 실무적 활용
RESTful API를 설계할 때 가장 중요한 부분 중 하나는 올바른 상태 코드를 반환하는 것이다.<br>
클라이언트는 서버가 제공하는 HTTP 상태 코드를 기반으로 응답을 해석하며, 올바른 상태 코드가 반환되지 않으면 오작동, 디버깅 문제, 예기치 않은 에러 발생 등의 문제가 생길 수 있다.

일반적으로 API 응답을 설계할 때는 다음과 같은 원칙을 따른다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트가 요청한 작업이 정상적으로 처리되었는지 명확히 전달할 것<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트가 오류를 받았을 때, 그 이유를 정확히 파악할 수 있도록 할 것<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;HTTP 상태 코드를 표준에 맞게 사용할 것<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;일관된 API 응답 패턴을 유지할 것

이제 각 상태 코드별로 구체적인 활용 사례를 살펴보겠다.

-------------------
### 200 OK - 일반적인 성공 응답
200 OK는 가장 흔하게 사용되는 HTTP 상태 코드이며, 요청이 성공적으로 처리되었음을 의미한다.<br>
**GET, PUT, PATCH, DELETE** 요청이 정상적으로 실행되었을 때 사용된다.
```java
@GetMapping("/users/{id}")
public ResponseEntity<User> getUser(@PathVariable Long id) {
    User user = userService.findById(id);
    
    if (user == null) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).build();
    }

    return ResponseEntity.ok(user);
}
```
위 코드에서는 ```GET /users/{id}``` 요청이 정상적으로 수행되었을 경우,<br>
```ResponseEntity.ok(user)```를 통해 HTTP 상태 코드 200 OK와 함께 데이터를 반환한다.

--------------------
### 201 Created - 리소스 생성 성공
201 Created는 POST 요청을 통해 새로운 리소스가 생성되었을 때 사용된다.<br>
이때, 반드시 응답 헤더에 생성된 리소스의 URL을 포함하는 것이 원칙이다.
```java
@PostMapping("/users")
public ResponseEntity<User> createUser(@RequestBody User user) {
    User savedUser = userService.save(user);
    URI location = URI.create("/users/" + savedUser.getId());

    return ResponseEntity.created(location).body(savedUser);
}
```
클라이언트가 새로운 유저를 생성하기 위해 ```POST /users``` 요청을 보낸다.<br>
서버는 201 Created 상태 코드와 함께 Location 헤더를 설정하여 생성된 리소스의 URL을 반환한다.

----------------
### 204 No Content - 응답 본문이 필요 없는 경우
204 No Content는 요청이 정상적으로 처리되었으나, 클라이언트에게 반환할 본문이 없을 때 사용된다.<br>
보통 DELETE 요청이 성공했을 때 사용된다.
```java
@DeleteMapping("/users/{id}")
public ResponseEntity<Void> deleteUser(@PathVariable Long id) {
    boolean deleted = userService.delete(id);

    if (!deleted) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).build();
    }

    return ResponseEntity.noContent().build();
}
```
클라이언트가 ```DELETE /users/{id}``` 요청을 보낸다.<br>
해당 사용자가 존재하면 삭제 후 204 No Content 응답을 보낸다.<br>
삭제할 사용자가 존재하지 않으면 404 Not Found를 반환한다.

-------------------
### 400 Bad Request - 잘못된 요청
400 Bad Request는 클라이언트가 보낸 요청이 잘못되었을 때 사용된다.<br>
예를 들어, 필수 필드가 누락되었거나, 잘못된 형식의 데이터가 포함된 경우 사용된다.
```java
@PostMapping("/users")
public ResponseEntity<String> createUser(@RequestBody @Valid User user, BindingResult result) {
    if (result.hasErrors()) {
        return ResponseEntity.status(HttpStatus.BAD_REQUEST)
                .body("잘못된 요청입니다: " + result.getAllErrors());
    }
    
    User savedUser = userService.save(user);
    return ResponseEntity.ok(savedUser);
}
```
클라이언트가 필수 입력 값을 빠뜨리고 POST /users 요청을 보냈을 경우,<br>
400 Bad Request 상태 코드와 함께 오류 메시지를 반환한다.

-------------------
### 401 Unauthorized - 인증 실패
401 Unauthorized는 클라이언트가 인증되지 않았을 때 발생한다.<br>
즉, API에 접근하려면 로그인 또는 인증 토큰이 필요하지만, 해당 정보를 제공하지 않았거나 잘못된 정보를 제공했을 경우 사용된다.
```java
@GetMapping("/secure-data")
public ResponseEntity<String> getSecureData(@RequestHeader(value = "Authorization", required = false) String authToken) {
    if (authToken == null || !authService.isValid(authToken)) {
        return ResponseEntity.status(HttpStatus.UNAUTHORIZED).body("인증이 필요합니다.");
    }

    return ResponseEntity.ok("보안 데이터입니다.");
}
```
Authorization 헤더 없이 요청을 보낼 경우 401 Unauthorized를 반환한다.

-----------------
### 403 Forbidden - 접근 권한 없음
403 Forbidden은 클라이언트가 인증은 되었지만, 특정 리소스에 대한 접근 권한이 없을 때 사용된다.
```java
@GetMapping("/admin")
public ResponseEntity<String> getAdminPage(@RequestHeader("Authorization") String token) {
    if (!authService.isAdmin(token)) {
        return ResponseEntity.status(HttpStatus.FORBIDDEN).body("접근 권한이 없습니다.");
    }

    return ResponseEntity.ok("관리자 페이지");
}
```
사용자가 일반 권한으로 관리자 페이지에 접근하려고 하면 403 Forbidden을 반환한다.

--------------------
### 404 Not Found - 리소스 없음
404 Not Found는 클라이언트가 요청한 리소스가 존재하지 않을 때 사용된다.<br>
예를 들어, 존재하지 않는 ID로 데이터를 조회하려는 경우 404가 반환된다.
```java
@GetMapping("/users/{id}")
public ResponseEntity<User> getUser(@PathVariable Long id) {
    return userService.findById(id)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.status(HttpStatus.NOT_FOUND).build());
}
```
사용자가 없는 ID로 요청하면 404 Not Found를 반환한다.

-------------------
### 500 Internal Server Error - 서버 내부 오류
500 Internal Server Error는 서버 내부에서 예기치 않은 오류가 발생했을 때 사용된다.<br>
보통, 예상하지 못한 예외가 발생했거나 서버에서 처리할 수 없는 오류가 있을 때 사용된다.
```java
@ExceptionHandler(Exception.class)
public ResponseEntity<String> handleException(Exception ex) {
    return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
            .body("서버 내부 오류 발생: " + ex.getMessage());
}
```
서버에서 예외가 발생하면 500 Internal Server Error를 반환하도록 설정한다.

--------------------
### 상태 코드 활용 시 주의할 점
**일관된 상태 코드 사용**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;API 내에서 같은 동작에 대해 다른 상태 코드를 사용하면 혼란을 초래할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, 리소스를 찾지 못했을 때 어떤 API는 404 Not Found를, 다른 API는 400 Bad Request를 반환하면 일관성이 떨어진다.

**필요 이상으로 상태 코드를 남발하지 말 것**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;상황에 맞게 적절한 상태 코드를 사용해야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, DELETE 요청이 성공적으로 처리되었는데 200 OK 대신 204 No Content를 사용하는 것이 더 적절하다.

**에러 메시지를 포함하여 반환할 것**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;상태 코드만 반환하면 클라이언트는 문제의 원인을 알 수 없다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JSON 형식으로 메시지를 포함하는 것이 좋다.

-----------------
## 2-3. 오류 응답 표준화
### 오류 응답의 필요성
RESTful API를 설계할 때 단순히 HTTP 상태 코드만 반환하는 것이 아니라, **일관된 형식의 오류 응답을 제공하는 것**이 중요하다.<br>
클라이언트는 API를 호출했을 때 **어떤 오류가 발생했는지, 어떻게 해결할 수 있는지**를 알아야 한다.

일반적으로 다음과 같은 이유로 오류 응답의 표준화가 필요하다.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**일관성 유지**: API마다 다른 오류 형식을 사용하면 클라이언트가 이를 처리하기 어려워진다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**디버깅 용이성**: 개발자와 사용자 모두 오류가 발생했을 때 문제를 쉽게 이해할 수 있어야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**자동화 및 로깅 지원**: 시스템이 오류를 수집하고 분석하기 위해서는 명확한 응답 형식이 필요하다.

표준화된 오류 응답을 사용하면 RESTful API의 가독성과 유지보수성이 크게 향상된다.

---------------------
### 오류 응답의 JSON 형식 설계
일반적으로 API의 오류 응답은 JSON 형식으로 제공되며, 다음과 같은 필드를 포함하는 것이 일반적이다.
```
{
  "timestamp": "2025-03-11T14:30:00Z",
  "status": 400,
  "error": "Bad Request",
  "message": "필수 필드 'email'이 누락되었습니다.",
  "path": "/users"
}
```
각 필드의 의미는 다음과 같다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```timestamp``` : 오류가 발생한 시점 (ISO 8601 형식)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```status``` : HTTP 상태 코드 (예: 400, 404, 500)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```error``` : 오류의 간략한 설명 (예: Bad Request, Unauthorized)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```message``` : 상세한 오류 메시지 (예: "필수 필드 'email'이 누락되었습니다.")<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```path``` : 오류가 발생한 API 엔드포인트 경로

위와 같은 응답 형식을 사용하면, 클라이언트가 오류를 보다 쉽게 처리할 수 있다.

------------------
### Spring Boot에서 오류 응답 표준화
Spring Boot에서는 ```@ControllerAdvice```를 사용하여 전역적으로 예외를 처리할 수 있다.<br>
이를 통해 일관된 오류 응답을 자동으로 생성할 수 있다.
```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<Map<String, Object>> handleValidationException(MethodArgumentNotValidException ex, HttpServletRequest request) {
        Map<String, Object> errorResponse = new HashMap<>();
        errorResponse.put("timestamp", Instant.now().toString());
        errorResponse.put("status", HttpStatus.BAD_REQUEST.value());
        errorResponse.put("error", "Bad Request");
        errorResponse.put("message", ex.getBindingResult().getAllErrors().get(0).getDefaultMessage());
        errorResponse.put("path", request.getRequestURI());

        return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(errorResponse);
    }

    @ExceptionHandler(EntityNotFoundException.class)
    public ResponseEntity<Map<String, Object>> handleNotFoundException(EntityNotFoundException ex, HttpServletRequest request) {
        Map<String, Object> errorResponse = new HashMap<>();
        errorResponse.put("timestamp", Instant.now().toString());
        errorResponse.put("status", HttpStatus.NOT_FOUND.value());
        errorResponse.put("error", "Not Found");
        errorResponse.put("message", ex.getMessage());
        errorResponse.put("path", request.getRequestURI());

        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(errorResponse);
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<Map<String, Object>> handleGenericException(Exception ex, HttpServletRequest request) {
        Map<String, Object> errorResponse = new HashMap<>();
        errorResponse.put("timestamp", Instant.now().toString());
        errorResponse.put("status", HttpStatus.INTERNAL_SERVER_ERROR.value());
        errorResponse.put("error", "Internal Server Error");
        errorResponse.put("message", "서버 내부 오류가 발생했습니다.");
        errorResponse.put("path", request.getRequestURI());

        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body(errorResponse);
    }
}
```
위 코드에서는 @RestControllerAdvice를 사용하여 전역 예외 처리 핸들러를 정의했다.

```MethodArgumentNotValidException``` : 유효성 검사 실패 시 400 Bad Request 응답을 반환한다.<br>
```EntityNotFoundException``` : 데이터가 존재하지 않을 경우 404 Not Found 응답을 반환한다.<br>
```Exception``` : 예상치 못한 서버 오류가 발생하면 500 Internal Server Error 응답을 반환한다.

이렇게 하면, 모든 API에서 동일한 형식의 오류 응답을 반환할 수 있다.

------------------------
### 클라이언트에서 오류 응답 처리하기
서버가 오류 응답을 표준화했다면, **클라이언트에서도 일관된 방식으로 오류를 처리하는 것이 중요하다.**<br>
예를 들어, React 또는 Vue.js와 같은 프론트엔드 애플리케이션에서 API 호출 시 오류를 처리하는 방법을 살펴보자.

JavaScript (React 예제)
```java
async function fetchUser(userId) {
    try {
        const response = await fetch(`/users/${userId}`);

        if (!response.ok) {
            const errorData = await response.json();
            throw new Error(`${errorData.status} ${errorData.message}`);
        }

        return await response.json();
    } catch (error) {
        console.error("API 요청 오류:", error.message);
        alert("오류 발생: " + error.message);
    }
}
```
위 코드는 API 호출 중 오류가 발생하면 서버가 반환한 JSON 오류 응답을 읽고, 클라이언트에서 처리할 수 있도록 한다.

--------------------------
### 오류 응답 표준화 시 주의할 점
**HTTP 상태 코드와 응답 메시지를 일치시켜야 한다.**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, 404 Not Found 응답을 보내면서 "Bad Request"라는 메시지를 제공하면 혼란을 초래할 수 있다.

**에러 메시지는 너무 자세하지 않아야 한다.**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;내부 서버 오류(500)와 같은 경우, 너무 많은 정보를 제공하면 보안에 취약할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"서버 내부 오류가 발생했습니다." 같은 일반적인 메시지를 사용하는 것이 좋다.

**모든 예외를 잡지 말고 적절한 예외만 처리해야 한다.**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, Exception.class를 전역적으로 처리하는 경우 모든 오류가 동일한 500으로 반환될 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;이를 방지하기 위해, 비즈니스 로직에서 발생하는 예외와 서버 내부 예외를 구분하는 것이 중요하다.

---------------------------------
# 3. API 버전 관리 전략
## 3-1. API 버전 관리 필요성
### API 버전 관리란?
API 버전 관리란 **API가 변경될 때 기존 사용자와의 호환성을 유지하면서 새로운 기능을 제공하는 방법**을 의미한다.<br>
API는 시간이 지남에 따라 변경될 수밖에 없으며, 기존 API 사용자의 기능을 보장하면서 새로운 API를 제공하는 것이 중요하다.

---------------
### API 버전 관리가 필요한 이유
API 버전 관리는 다음과 같은 이유로 필수적이다.

**하위 호환성 유지**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;API 변경이 기존 사용자에게 영향을 미치지 않도록 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트가 오래된 API를 사용해도 서비스가 중단되지 않도록 해야 한다.

**API 확장 가능성 제공**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;기존 API에 새로운 기능을 추가할 수 있어야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;새로운 기능을 도입하면서도 기존 기능을 유지할 방법이 필요하다.

**다양한 클라이언트 지원**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;웹, 모바일, 데스크톱 등 다양한 클라이언트가 API를 사용하며, 각기 다른 버전을 요구할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;특정 클라이언트가 구 버전을 계속 사용할 수 있도록 보장해야 한다.

**서비스 안정성 보장**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;API 변경이 예측 가능해야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;갑작스러운 API 변경은 클라이언트의 장애를 초래할 수 있으므로 사전에 버전 업그레이드를 계획해야 한다.

----------------
### API 버전 관리를 하지 않을 경우 발생하는 문제
API 버전 관리를 하지 않으면 다음과 같은 문제가 발생할 수 있다.

**예기치 않은 서비스 중단**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;새로운 API가 기존 API를 덮어씌우면 클라이언트가 더 이상 요청을 보낼 수 없게 된다.

**클라이언트와의 충돌**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;특정 필드를 삭제하거나 변경하면 기존 클라이언트 코드가 깨질 수 있다.

**비효율적인 API 운영**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;구 API와 신 API가 뒤섞여 복잡성이 증가할 수 있다.

------------------
### API 변경 유형
API 변경은 보통 다음과 같은 두 가지 방식으로 구분할 수 있다.

**하위 호환성을 유지하는 변경 (Backward Compatible Changes)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;새로운 필드 추가<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;기존 필드 유지<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;응답 형식을 변경하지 않음

예제 (하위 호환 유지 예시):
```
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com",
  "phone": "010-1234-5678"
}
```
위 API 응답에 ```"phone"``` 필드가 추가되었지만, 기존 클라이언트는 "id", "name", "email" 필드만 사용하므로 문제없이 동작할 수 있다.

**하위 호환성을 깨뜨리는 변경 (Breaking Changes)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;필드 제거<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;응답 구조 변경<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;API 엔드포인트 변경

예제 (하위 호환 깨짐 예시):
```
{
  "userId": 1,
  "fullName": "John Doe",
  "contact": {
    "email": "john@example.com",
    "phone": "010-1234-5678"
  }
}
```
기존 "id", "name" 필드가 "userId", "fullName"으로 변경되었고 "contact" 구조가 추가되었기 때문에, 이전 클라이언트에서는 API 응답을 정상적으로 파싱하지 못할 수 있다.

이런 경우, 새로운 API 버전을 제공하여 기존 클라이언트가 문제없이 기존 API를 사용할 수 있도록 해야 한다.

----------------
### API 버전 관리의 핵심 원칙
**기존 API는 최대한 변경하지 않는다.**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;기존 클라이언트가 문제없이 사용할 수 있도록 유지해야 한다.<br>

**새로운 버전을 제공할 때는 명확한 기준을 따른다.**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트가 어떤 API 버전을 사용하고 있는지 알 수 있어야 한다.

**버전 지원 중단(EOL, End-of-Life) 정책을 정한다.**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;모든 버전을 무기한 지원할 수는 없으므로, 일정 시간이 지나면 구 버전을 폐기하는 정책이 필요하다.

---------------------
## 3-2. API 변경 시 고려 사항
### 하위 호환성을 유지하는 방법
API를 변경할 때 기존 사용자가 계속해서 API를 사용할 수 있도록 하위 호환성을 유지하는 것이 중요하다. 하위 호환성을 유지하는 방법에는 다음과 같은 기법이 있다.

**기존 필드 변경을 피하기*<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;기존 필드의 이름이나 데이터 타입을 변경하면 클라이언트 코드가 깨질 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;따라서 기존 필드는 변경하지 않고 새로운 필드를 추가하는 방식으로 확장해야 한다.

예제 (필드 추가 - 하위 호환 유지) :
```
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com",
  "phone": "010-1234-5678"
}
```
위 API에 "phone" 필드를 추가하더라도, 기존 클라이언트는 영향을 받지 않고 동작할 수 있다.

**기존 API 구조를 유지하면서 확장하기**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;응답 필드를 추가할 경우, 기존 구조를 유지하면서 새로운 기능을 도입한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JSON 응답을 중첩 구조로 변경하는 경우, 기존 구조를 유지하는 것이 중요하다.

예제 (하위 호환 깨짐 - 변경된 구조) :
```
{
  "userId": 1,
  "fullName": "John Doe",
  "contact": {
    "email": "john@example.com",
    "phone": "010-1234-5678"
  }
}
```
기존 클라이언트는 "id"와 "name" 필드를 찾을 수 없으므로 API 응답을 정상적으로 처리하지 못할 가능성이 있다.

올바른 방식 (기존 구조 유지 + 확장 가능하도록 추가) :
```
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com",
  "phone": "010-1234-5678",
  "contact": {
    "email": "john@example.com",
    "phone": "010-1234-5678"
  }
}
```
기존 필드를 유지하면서 새로운 contact 객체를 추가하면 기존 클라이언트도 문제없이 동작할 수 있다.

**응답 데이터의 기본값을 설정하기**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;새로운 필드를 추가할 경우, 기본값을 설정하여 예기치 않은 오류를 방지해야 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;null 값이 반환되지 않도록 기본값을 설정하면 클라이언트의 예외 처리를 간소화할 수 있다.

예제 (기본값 설정) :
```
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com",
  "isVerified": false
}
```
"isVerified" 필드를 새롭게 추가했지만 기본값을 false로 설정하여 클라이언트에서 오류가 발생하지 않도록 처리할 수 있다.

-------------------
### 버전 업그레이드 전략
API 버전 업그레이드는 다음과 같은 전략을 따르는 것이 일반적이다.

**새로운 버전을 병렬로 제공**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;/v1/users → /v2/users 처럼 새로운 버전을 제공하여 기존 사용자가 영향을 받지 않도록 한다.

**구버전 유지 기간을 설정**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;일정 기간 동안 구버전을 유지하면서 새로운 버전으로의 전환을 유도한다.

**API 변경 로그(Changelog) 제공**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;API가 어떻게 변경되었는지 문서화하고 사용자에게 공지해야 한다.

**기존 API의 Deprecation 안내**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;더 이상 사용하지 않는 API는 Deprecation Notice를 포함하여 일정 기간 후 폐기될 것임을 알린다.

--------------------
# 4. HATEOAS(Hypermedia as the Engine of Application State)
## 4-1. HATEOAS 개념과 필요성
### HATEOAS 개념
HATEOAS(Hypermedia as the Engine of Application State)는 REST API에서 중요한 개념 중 하나로, 클라이언트가 사전에 API의 동작을 알지 않아도, API 응답에서 제공되는 하이퍼미디어 링크를 통해 동적으로 API를 탐색할 수 있도록 하는 원칙이다.

즉, HATEOAS는 API 응답에서 해당 리소스와 관련된 추가적인 정보를 담은 링크를 제공하여, 클라이언트가 서버와 상호작용할 수 있도록 한다.

HATEOAS를 적용하면 API 소비자가 사전에 특정 URL을 알고 있을 필요 없이, 응답에 포함된 링크를 따라가면서 필요한 작업을 수행할 수 있다. 이는 클라이언트와 서버 간의 결합도를 낮추고, API의 유연성과 유지보수성을 향상시킨다.

### HATEOAS의 필요성
HATEOAS는 단순한 REST API보다 한 단계 더 발전된 RESTful API를 제공하며, 다음과 같은 이유로 필요하다.

**서버와 클라이언트 간의 결합도를 낮춘다**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;API 엔드포인트가 변경되더라도 클라이언트가 이를 미리 알 필요 없이 동적으로 API를 탐색할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;서버가 API 응답에 링크를 포함하면, 클라이언트는 그 링크를 이용해 API를 호출할 수 있다.

**API 사용성을 향상시킨다**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트는 API 응답에 포함된 링크를 이용하여 가능한 액션을 쉽게 파악할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;사용자는 API의 내부 로직을 알 필요 없이 링크를 통해 필요한 기능을 사용할 수 있다.

**API의 유지보수가 용이해진다**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;새로운 기능을 추가할 때, 기존 API 구조를 변경하지 않고도 새로운 링크를 추가함으로써 기능 확장이 가능하다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;기존의 클라이언트도 문제없이 동작하면서 새로운 기능을 점진적으로 도입할 수 있다.

**RESTful API의 본질을 유지한다**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;REST의 원칙 중 하나인 Self-descriptive messages(자체 기술 메시지) 개념을 적용하여, API 응답 자체가 사용 방법을 포함하게 된다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;API 사용자는 문서를 확인하지 않고도 제공된 링크를 통해 API의 동작을 이해할 수 있다.

---------------
### HATEOAS를 적용한 API 응답 예시
다음은 HATEOAS를 적용한 API 응답 예제이다.

예제 (일반적인 API 응답 - HATEOAS 미적용)
```
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com"
}
```
위 API 응답에서는 클라이언트가 사용자의 정보를 조회할 수 있지만, 사용자가 다른 동작(예: 수정, 삭제)을 수행하려면 해당 API의 엔드포인트를 미리 알고 있어야 한다.

예제 (HATEOAS 적용 API 응답)
```
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com",
  "_links": {
    "self": {
      "href": "https://api.example.com/users/1"
    },
    "update": {
      "href": "https://api.example.com/users/1",
      "method": "PUT"
    },
    "delete": {
      "href": "https://api.example.com/users/1",
      "method": "DELETE"
    }
  }
}
```
## 4-2. REST API에서 Hypermedia 적용 방식
### Hypermedia 적용 방식 개요
REST API에서 Hypermedia를 적용하는 방식은 API의 응답에 링크 정보를 포함하여 클라이언트가 추가적인 작업을 쉽게 수행할 수 있도록 하는 것이다. 이는 서버가 리소스 상태와 관련된 액션을 명시적으로 제공하는 방식으로, 클라이언트는 사전에 엔드포인트 정보를 몰라도 API 응답을 통해 자연스럽게 API 탐색이 가능하도록 한다.

Hypermedia 적용 방식은 다음과 같은 원칙을 따른다.

**Self-Descriptive API (자체 기술 API)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트가 API 응답만 보고도 추가적으로 수행할 수 있는 동작을 이해할 수 있도록 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, 특정 리소스가 활성 상태일 때만 수정 가능하고, 비활성 상태에서는 삭제만 가능하도록 API 응답에 이를 반영할 수 있다.

**Link-Driven API (링크 기반 API 탐색)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;API 응답에 포함된 _links 항목을 통해 현재 상태에서 가능한 작업을 제공한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트는 별도의 문서 없이 응답을 분석하여 API 흐름을 이해할 수 있다.

**상태 변화에 따른 동적 링크 제공**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;리소스의 상태가 변함에 따라 제공되는 링크도 동적으로 변경된다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, 주문이 "결제 대기" 상태일 때는 "결제하기" 링크를 제공하고, "배송 중" 상태일 때는 "배송 추적" 링크를 제공할 수 있다.

--------------
### Hypermedia 적용 방식의 주요 패턴
Hypermedia를 적용하는 대표적인 방법에는 HAL(Hypertext Application Language), JSON:API, Siren, Collection+JSON 등의 포맷이 있다. 이들 포맷을 활용하면 REST API의 응답에 링크를 체계적으로 포함할 수 있다.

------------------
### HAL(Hypertext Application Language) 적용 예시
HAL(Hypertext Application Language)은 REST API에서 하이퍼미디어 요소를 포함하기 위한 JSON 기반의 표준 포맷이다. 다음은 HAL을 적용한 API 응답 예제이다.
```
{
  "_links": {
    "self": {
      "href": "https://api.example.com/orders/1"
    },
    "customer": {
      "href": "https://api.example.com/customers/42"
    },
    "payment": {
      "href": "https://api.example.com/orders/1/payment"
    },
    "cancel": {
      "href": "https://api.example.com/orders/1/cancel",
      "method": "DELETE"
    }
  },
  "id": 1,
  "status": "pending",
  "total_price": 100.00
}
```
위 응답을 해석하면 다음과 같은 특징을 가진다.

```_links.self```: 현재 리소스의 URI 제공<br>
```_links.customer```: 관련 고객 정보를 조회할 수 있는 URI 제공<br>
```_links.payment```: 결제를 수행할 수 있는 URI 제공<br>
```_links.cancel```: 주문을 취소할 수 있는 URI 제공 (HTTP DELETE 요청 필요)

이런 방식으로 API가 동작하면 클라이언트는 별도의 엔드포인트 정보를 사전에 몰라도, API 응답을 보고 적절한 액션을 수행할 수 있다.

### JSON:API 적용 예시
JSON:API는 데이터와 관련된 링크를 보다 체계적으로 관리할 수 있도록 설계된 포맷이다.
```
{
  "data": {
    "type": "orders",
    "id": "1",
    "attributes": {
      "status": "pending",
      "total_price": 100.00
    },
    "relationships": {
      "customer": {
        "links": {
          "related": "https://api.example.com/customers/42"
        }
      }
    }
  },
  "links": {
    "self": "https://api.example.com/orders/1"
  }
}
```
JSON:API 방식은 데이터를 data 필드 내에서 관리하고, relationships 항목을 통해 관련 리소스와의 관계를 링크로 표현하는 것이 특징이다.

------------------
### Spring Boot에서 Hypermedia 적용
Spring Boot에서는 Spring HATEOAS 라이브러리를 사용하여 Hypermedia를 적용할 수 있다.

Spring Boot 프로젝트에 HATEOAS 추가
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-hateoas</artifactId>
</dependency>
```
Spring HATEOAS를 적용한 컨트롤러 예제
```java
@RestController
@RequestMapping("/orders")
public class OrderController {

    @GetMapping("/{id}")
    public EntityModel<Order> getOrder(@PathVariable Long id) {
        Order order = new Order(id, "pending", 100.00);

        EntityModel<Order> model = EntityModel.of(order,
                WebMvcLinkBuilder.linkTo(WebMvcLinkBuilder.methodOn(OrderController.class).getOrder(id)).withSelfRel(),
                WebMvcLinkBuilder.linkTo(WebMvcLinkBuilder.methodOn(CustomerController.class).getCustomer(42L)).withRel("customer"),
                WebMvcLinkBuilder.linkTo(WebMvcLinkBuilder.methodOn(OrderController.class).cancelOrder(id)).withRel("cancel"));

        return model;
    }

    @DeleteMapping("/{id}/cancel")
    public ResponseEntity<?> cancelOrder(@PathVariable Long id) {
        return ResponseEntity.noContent().build();
    }
}
```

Spring HATEOAS가 적용된 응답 예제
```
{
  "id": 1,
  "status": "pending",
  "total_price": 100.00,
  "_links": {
    "self": {
      "href": "http://localhost:8080/orders/1"
    },
    "customer": {
      "href": "http://localhost:8080/customers/42"
    },
    "cancel": {
      "href": "http://localhost:8080/orders/1/cancel"
    }
  }
}
```
위와 같이 Spring HATEOAS를 적용하면 API 응답에서 클라이언트가 추가적인 액션을 수행할 수 있도록 적절한 링크를 포함할 수 있다.

--------------------
## 4-3. Spring HATEOAS를 활용한 API 설계
### Spring HATEOAS란?
Spring HATEOAS는 Spring Boot 기반의 애플리케이션에서 REST API 응답에 하이퍼미디어(Hypermedia)를 손쉽게 적용할 수 있도록 도와주는 라이브러리이다. 이를 활용하면 REST API 응답이 단순한 JSON 데이터가 아니라, 클라이언트가 추가적인 API 탐색과 동작 수행을 할 수 있도록 링크 정보를 포함할 수 있다.

Spring HATEOAS의 주요 특징은 다음과 같다.

EntityModel을 통한 단일 리소스 모델 지원

REST API 응답에서 단일 객체를 감싸고, 해당 리소스와 관련된 링크를 추가할 수 있다.
CollectionModel을 통한 다중 리소스 모델 지원

다수의 엔티티를 반환할 때, 관련된 링크들을 함께 제공할 수 있다.
WebMvcLinkBuilder를 활용한 링크 자동 생성

Spring MVC 컨트롤러 메서드를 기반으로 하이퍼미디어 링크를 동적으로 생성할 수 있다.
링크 기반 API 응답 제공

API 응답에서 self, next, prev, related 등 다양한 링크를 포함할 수 있다.
Spring HATEOAS 설정
Spring Boot에서 HATEOAS를 적용하려면 spring-boot-starter-hateoas 의존성을 추가해야 한다.

Maven 프로젝트의 경우

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-hateoas</artifactId>
</dependency>
Gradle 프로젝트의 경우

implementation 'org.springframework.boot:spring-boot-starter-hateoas'
이제 Spring Boot에서 HATEOAS를 적용하여 REST API 응답을 개선하는 방법을 살펴보자.

EntityModel을 활용한 단일 리소스 응답
Spring HATEOAS에서 단일 리소스의 응답을 생성할 때는 EntityModel<T> 클래스를 활용한다. EntityModel<T>는 단일 객체와 함께 해당 객체에 대한 링크를 포함할 수 있도록 지원한다.

다음은 Order 객체를 예제로 사용하는 코드이다.

Order 엔티티

public class Order {
    private Long id;
    private String status;
    private Double totalPrice;

    public Order(Long id, String status, Double totalPrice) {
        this.id = id;
        this.status = status;
        this.totalPrice = totalPrice;
    }

    public Long getId() { return id; }
    public String getStatus() { return status; }
    public Double getTotalPrice() { return totalPrice; }
}
OrderController에서 단일 리소스 응답 생성

@RestController
@RequestMapping("/orders")
public class OrderController {

    @GetMapping("/{id}")
    public EntityModel<Order> getOrder(@PathVariable Long id) {
        Order order = new Order(id, "pending", 100.00);

        EntityModel<Order> model = EntityModel.of(order,
                WebMvcLinkBuilder.linkTo(WebMvcLinkBuilder.methodOn(OrderController.class).getOrder(id)).withSelfRel(),
                WebMvcLinkBuilder.linkTo(WebMvcLinkBuilder.methodOn(CustomerController.class).getCustomer(42L)).withRel("customer"),
                WebMvcLinkBuilder.linkTo(WebMvcLinkBuilder.methodOn(OrderController.class).cancelOrder(id)).withRel("cancel"));

        return model;
    }

    @DeleteMapping("/{id}/cancel")
    public ResponseEntity<?> cancelOrder(@PathVariable Long id) {
        return ResponseEntity.noContent().build();
    }
}
EntityModel을 활용한 응답 예시
위와 같은 설정으로 /orders/1 엔드포인트를 호출하면 다음과 같은 응답이 반환된다.

{
  "id": 1,
  "status": "pending",
  "total_price": 100.00,
  "_links": {
    "self": {
      "href": "http://localhost:8080/orders/1"
    },
    "customer": {
      "href": "http://localhost:8080/customers/42"
    },
    "cancel": {
      "href": "http://localhost:8080/orders/1/cancel"
    }
  }
}
이와 같이 응답에 하이퍼미디어 링크가 포함되어 있어 클라이언트가 추가적인 동작을 쉽게 수행할 수 있도록 한다.

CollectionModel을 활용한 다중 리소스 응답
CollectionModel<T>은 여러 개의 리소스를 포함하는 응답을 만들 때 사용된다. 여러 개의 Order 데이터를 반환하면서 각 리소스에 대한 링크를 포함할 수 있다.

OrderController에서 다중 리소스 응답 생성

@GetMapping
public CollectionModel<EntityModel<Order>> getAllOrders() {
    List<EntityModel<Order>> orders = List.of(
            EntityModel.of(new Order(1L, "pending", 100.00),
                    WebMvcLinkBuilder.linkTo(WebMvcLinkBuilder.methodOn(OrderController.class).getOrder(1L)).withSelfRel()),
            EntityModel.of(new Order(2L, "shipped", 150.00),
                    WebMvcLinkBuilder.linkTo(WebMvcLinkBuilder.methodOn(OrderController.class).getOrder(2L)).withSelfRel())
    );

    return CollectionModel.of(orders,
            WebMvcLinkBuilder.linkTo(WebMvcLinkBuilder.methodOn(OrderController.class).getAllOrders()).withSelfRel());
}
CollectionModel을 활용한 응답 예시
위와 같은 설정으로 /orders 엔드포인트를 호출하면 다음과 같은 응답이 반환된다.

{
  "_embedded": {
    "orders": [
      {
        "id": 1,
        "status": "pending",
        "total_price": 100.00,
        "_links": {
          "self": {
            "href": "http://localhost:8080/orders/1"
          }
        }
      },
      {
        "id": 2,
        "status": "shipped",
        "total_price": 150.00,
        "_links": {
          "self": {
            "href": "http://localhost:8080/orders/2"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "http://localhost:8080/orders"
    }
  }
}
이제 클라이언트는 각 주문에 대한 상세 정보를 self 링크를 통해 조회할 수 있다.

Spring HATEOAS 적용의 장점
API 유연성 증가

클라이언트가 사전에 엔드포인트를 몰라도 API 응답을 기반으로 동적으로 요청을 수행할 수 있다.
API 유지보수성 향상

API 변경 시, 클라이언트는 링크를 따라가기만 하면 되므로 엔드포인트 변경에도 영향을 덜 받는다.
RESTful 원칙 준수

HATEOAS를 적용하면 RESTful의 핵심 원칙 중 하나인 Self-descriptive Messages(자체 기술 메시지) 원칙을 만족할 수 있다.
5. RESTful API 보안 기초
5.1. API 보안 개요
API 보안이 중요한 이유
API(Application Programming Interface)는 클라이언트와 서버 간의 데이터를 주고받는 중요한 인터페이스이다. 하지만 API가 보안 설정 없이 운영될 경우, 악의적인 공격자로부터 해킹, 데이터 조작, 불법 접근 등의 위협을 받을 가능성이 크다.

API 보안이 중요한 이유는 다음과 같다.

데이터 보호

API를 통해 주고받는 데이터에는 개인정보, 결제 정보, 기업의 내부 데이터 등이 포함될 수 있다. 적절한 보안 조치를 취하지 않으면 민감한 정보가 유출될 위험이 있다.
인증 및 권한 관리

사용자별로 접근할 수 있는 데이터가 다를 수 있으며, 불법적인 접근을 방지해야 한다. 이를 위해 인증(Authentication) 및 권한 관리(Authorization)가 필요하다.
API 남용 방지

API를 무차별적으로 호출하는 공격(예: DoS, Brute Force 공격)을 방지해야 한다. API 호출 횟수를 제한하거나 IP 기반의 접근 제어를 적용할 수 있다.
데이터 조작 방지

API 요청을 위조하여 데이터를 변경하는 공격(SQL Injection, JSON Manipulation 등)을 차단해야 한다.
CORS 및 네트워크 보안

다른 도메인에서의 API 호출을 차단하는 CORS 정책을 설정하고, HTTPS를 이용한 보안을 강화해야 한다.
API 보안 위협 요소
API가 직면할 수 있는 주요 보안 위협 요소를 살펴보자.

무차별 대입 공격(Brute Force Attack)

공격자가 API의 인증 시스템을 무작위로 대입하여 로그인 시도를 반복하는 방식의 공격이다. 예를 들어, 특정 사용자의 비밀번호를 추측하기 위해 수천 번의 요청을 시도할 수 있다.
SQL Injection

공격자가 API 요청의 파라미터에 SQL 문을 삽입하여 데이터베이스를 조작하는 공격이다.
예: GET /users?id=1 OR 1=1 와 같은 요청을 통해 모든 사용자 정보를 조회할 수 있다.
XSS (Cross-Site Scripting) 공격

API의 응답에서 HTML 또는 JavaScript 코드가 실행되도록 조작하여, 사용자의 브라우저에서 악성 코드가 실행되도록 하는 공격이다.
CSRF (Cross-Site Request Forgery) 공격

사용자가 로그인된 상태에서 악의적인 웹사이트에 접근하면, 공격자가 사용자의 인증 정보를 이용해 API 요청을 보내는 방식이다.
데이터 스니핑(Data Sniffing)

네트워크에서 API 요청과 응답을 가로채어 데이터를 탈취하는 공격이다. HTTPS를 사용하지 않는 경우 이러한 위험이 커진다.
API 보안을 위한 주요 방어 전략
API 보안을 강화하기 위해 다음과 같은 전략을 적용할 수 있다.

인증(Authentication) 및 권한 관리(Authorization) 적용

API 호출 시 반드시 인증을 요구하고, 사용자별로 권한을 관리해야 한다.
OAuth 2.0, JWT(Json Web Token), API Key 등의 인증 방식을 활용할 수 있다.
HTTPS 적용

API와 클라이언트 간의 데이터 전송을 암호화하기 위해 반드시 HTTPS를 사용해야 한다.
이를 통해 데이터 스니핑 공격을 방지할 수 있다.
CORS 설정

다른 도메인에서 API를 호출하지 못하도록 CORS(Cross-Origin Resource Sharing) 정책을 설정해야 한다.
API Rate Limiting (요청 횟수 제한)

특정 기간 동안 API를 호출할 수 있는 횟수를 제한하여 무차별 대입 공격을 방어할 수 있다.
예: 사용자가 1분에 100번 이상의 요청을 보내면 차단.
입력 값 검증

API 요청에서 전달되는 모든 데이터를 철저하게 검증해야 한다.
SQL Injection과 같은 공격을 방지하기 위해 Prepared Statement를 사용하고, XSS 공격을 방어하기 위해 HTML Escape 처리를 수행해야 한다.
로그 및 모니터링 시스템 구축

API 호출 기록을 로깅하고, 의심스러운 활동을 모니터링하여 이상 징후가 감지되면 즉시 대응해야 한다.
Spring Boot에서 기본적인 API 보안 적용 방법
Spring Boot에서 API 보안을 적용하는 간단한 예제를 살펴보자.

1. HTTPS 적용 Spring Boot에서 HTTPS를 활성화하려면 application.properties 또는 application.yml 설정 파일에서 HTTPS를 활성화해야 한다.

server.port=8443
server.ssl.key-store=classpath:keystore.p12
server.ssl.key-store-password=yourpassword
server.ssl.key-store-type=PKCS12
server.ssl.key-alias=tomcat
이렇게 하면 API가 HTTP가 아닌 HTTPS를 통해서만 접근 가능하게 된다.

2. JWT 기반 인증 적용 Spring Boot에서 JWT(Json Web Token)를 이용한 인증을 적용하는 방법을 간단히 살펴보자.

JWT 인증 필터

public class JwtAuthenticationFilter extends OncePerRequestFilter {

    private final JwtTokenProvider jwtTokenProvider;

    public JwtAuthenticationFilter(JwtTokenProvider jwtTokenProvider) {
        this.jwtTokenProvider = jwtTokenProvider;
    }

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)
            throws ServletException, IOException {
        String token = jwtTokenProvider.resolveToken(request);
        if (token != null && jwtTokenProvider.validateToken(token)) {
            Authentication auth = jwtTokenProvider.getAuthentication(token);
            SecurityContextHolder.getContext().setAuthentication(auth);
        }
        filterChain.doFilter(request, response);
    }
}
이제 API를 호출할 때, JWT 토큰이 없는 요청은 거부할 수 있다.

3. CORS 설정 적용 Spring Boot에서 CORS 정책을 설정하려면 WebMvcConfigurer를 구현하면 된다.
```java
@Configuration
public class CorsConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/api/**")
                .allowedOrigins("https://trusted-domain.com")
                .allowedMethods("GET", "POST", "PUT", "DELETE")
                .allowCredentials(true);
    }
}
```
이렇게 하면 https://trusted-domain.com에서만 API 호출을 허용할 수 있다.

-----------------
### API 보안 적용 시 주의할 점
API 보안을 적용할 때 다음 사항을 반드시 고려해야 한다.

보안은 다층 방어 전략이 필요하다

단순히 JWT 인증만 적용하는 것이 아니라, HTTPS, Rate Limiting, SQL Injection 방어 등의 다양한 보안 기술을 병행해야 한다.
모든 API 엔드포인트에 대해 인증 및 권한 검사를 수행해야 한다

API Key 또는 JWT가 없다면 API를 호출할 수 없도록 해야 한다.
로그와 모니터링을 강화해야 한다

의심스러운 API 호출을 실시간으로 감지하고 차단할 수 있도록 로그 및 모니터링 시스템을 구축해야 한다.
학습자의 사고를 돕기 위한 질문
API를 보호하지 않으면 발생할 수 있는 주요 보안 위협은 무엇인가?

데이터 유출, 무단 접근, 악성 공격을 고려해보라.
API 보안을 강화하기 위해 일반적으로 적용하는 주요 보안 기법은 무엇인가?

인증, 권한 부여, 데이터 암호화와 같은 개념을 떠올려보라.
5.2. 인증(Authentication)과 권한 부여(Authorization)
인증(Authentication)과 권한 부여(Authorization)의 차이
RESTful API 보안을 강화하기 위해서는 인증(Authentication)과 권한 부여(Authorization)를 정확히 이해하고 적용해야 한다.

인증 (Authentication) :

API를 호출하는 사용자가 누구인지 확인하는 과정이다.
일반적으로 로그인 과정에서 사용되며, 사용자의 아이디 및 비밀번호를 확인하거나 OAuth, API 키, JWT 토큰을 활용할 수 있다.
예를 들어, 사용자가 특정 API를 호출할 때 유효한 JWT 토큰을 제공해야 한다면, 이는 인증 과정에 해당한다.
권한 부여 (Authorization) :

인증된 사용자가 특정 API에 접근할 권한이 있는지 확인하는 과정이다.
예를 들어, 관리자(Admin)만 특정 리소스를 수정할 수 있도록 설정하는 것이 권한 부여의 예시이다.
역할 기반 접근 제어(RBAC) 또는 속성 기반 접근 제어(ABAC)를 활용하여 권한을 설정할 수 있다.
인증 방식의 종류
RESTful API에서 사용되는 주요 인증 방식을 살펴보자.

Basic Authentication (기본 인증)

HTTP Authorization 헤더를 사용하여 사용자 이름과 비밀번호를 Base64로 인코딩하여 전달하는 방식이다.
보안성이 낮으며, HTTPS 없이 사용하면 위험하다.
Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=
단점:
비밀번호가 그대로 노출될 위험이 있음.
클라이언트가 매 요청마다 사용자 정보를 보내야 함.
HTTPS 없이 사용하면 취약점이 발생할 가능성이 높음.
API Key 인증

사용자가 API를 호출할 때 고유한 API 키를 포함하여 요청을 보내는 방식이다.
GET /users HTTP/1.1
Host: api.example.com
x-api-key: your-api-key-here
장점:
간단한 구현이 가능하며, 서버에서 API 키를 통해 요청을 검증할 수 있음.
단점:
API 키가 유출되면 누구나 API를 사용할 수 있음.
요청마다 API 키를 포함해야 하므로 보안적인 단점이 존재.
OAuth 2.0 (Open Authorization)

제3자 인증을 지원하는 표준 프로토콜로, 구글, 페이스북 등의 서비스에서 많이 사용된다.
OAuth 2.0은 access_token을 발급받아 API를 호출하는 방식이다.
Authorization: Bearer your-access-token-here
장점:
비밀번호를 직접 저장하지 않아도 됨.
API 접근 권한을 세밀하게 관리할 수 있음.
단점:
구현이 복잡하며, 인증 서버를 구축해야 함.
JWT (JSON Web Token)

JWT는 JSON 기반의 토큰을 사용하여 인증과 권한 부여를 처리하는 방식이다.
서버에서 로그인 성공 시 JWT를 발급하고, 클라이언트는 이후 요청에서 이 토큰을 Authorization 헤더에 포함하여 보낸다.
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
장점:
Stateless(무상태) 방식으로, 서버에서 세션을 유지할 필요가 없음.
토큰에 사용자 정보를 포함할 수 있어 API 요청 시 추가적인 데이터베이스 조회를 줄일 수 있음.
단점:
토큰이 탈취되면 악용될 위험이 있음.
토큰을 안전하게 저장해야 하며, 만료된 토큰을 처리하는 로직이 필요함.
Spring Boot에서 JWT 기반 인증 구현
Spring Boot에서 JWT 기반 인증을 구현하는 방법을 간단히 살펴보자.

1. JWT 토큰 생성하기 JWT 토큰을 생성하는 JwtTokenProvider 클래스를 정의한다.

import io.jsonwebtoken.*;
import io.jsonwebtoken.security.Keys;
import org.springframework.stereotype.Component;
import java.util.Date;

@Component
public class JwtTokenProvider {
    private final String secretKey = "your-secret-key-your-secret-key"; // 안전한 키를 사용해야 함.
    private final long validityInMilliseconds = 3600000; // 1시간

    public String createToken(String username) {
        return Jwts.builder()
                .setSubject(username)
                .setIssuedAt(new Date())
                .setExpiration(new Date(System.currentTimeMillis() + validityInMilliseconds))
                .signWith(Keys.hmacShaKeyFor(secretKey.getBytes()), SignatureAlgorithm.HS256)
                .compact();
    }

    public boolean validateToken(String token) {
        try {
            Jwts.parserBuilder().setSigningKey(secretKey.getBytes()).build().parseClaimsJws(token);
            return true;
        } catch (JwtException | IllegalArgumentException e) {
            return false;
        }
    }
}
2. JWT 인증 필터 생성 JWT 토큰을 요청에서 추출하여 인증하는 필터를 생성한다.

import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.web.filter.OncePerRequestFilter;
import javax.servlet.FilterChain;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class JwtAuthenticationFilter extends OncePerRequestFilter {

    private final JwtTokenProvider jwtTokenProvider;

    public JwtAuthenticationFilter(JwtTokenProvider jwtTokenProvider) {
        this.jwtTokenProvider = jwtTokenProvider;
    }

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)
            throws ServletException, IOException {
        String token = resolveToken(request);
        if (token != null && jwtTokenProvider.validateToken(token)) {
            SecurityContextHolder.getContext().setAuthentication(jwtTokenProvider.getAuthentication(token));
        }
        filterChain.doFilter(request, response);
    }

    private String resolveToken(HttpServletRequest request) {
        String bearerToken = request.getHeader("Authorization");
        if (bearerToken != null && bearerToken.startsWith("Bearer ")) {
            return bearerToken.substring(7);
        }
        return null;
    }
}
권한 부여 (Authorization) 적용
Spring Security를 활용하여 역할(Role)에 따라 API 접근을 제한할 수 있다.
예를 들어, /admin 경로는 관리자만 접근할 수 있도록 설정할 수 있다.

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .csrf().disable()
            .authorizeRequests()
            .antMatchers("/admin/**").hasRole("ADMIN")
            .antMatchers("/user/**").hasAnyRole("USER", "ADMIN")
            .anyRequest().authenticated()
            .and()
            .httpBasic(); // 테스트용 설정

        return http.build();
    }
}
이렇게 하면:

/admin/** 경로는 관리자(ADMIN)만 접근 가능하다.
/user/** 경로는 일반 사용자(USER) 및 관리자(ADMIN) 모두 접근 가능하다.
인증 및 권한 부여 시 고려해야 할 보안 사항
JWT 토큰을 안전한 장소에 저장해야 한다.

브라우저에서는 localStorage가 아닌 HttpOnly 쿠키를 사용해야 한다.
모바일 앱에서는 안전한 저장소(SecureStorage)를 활용해야 한다.
토큰의 만료 시간을 적절히 설정해야 한다.

너무 짧으면 사용자가 자주 재로그인을 해야 한다.
너무 길면 보안 위험이 증가한다.
관리자 권한을 조심히 부여해야 한다.

기본적으로 모든 사용자는 USER 권한을 부여받고, 추가적인 역할이 필요하면 검증된 사용자에게만 ADMIN을 부여해야 한다.
5.3. CORS(Cross-Origin Resource Sharing) 정책
CORS 개념과 문제점
CORS(Cross-Origin Resource Sharing)는 웹 애플리케이션이 다른 도메인의 리소스를 요청할 때 발생하는 보안 정책이다.
웹 브라우저는 보안상의 이유로 동일 출처 정책(Same-Origin Policy)을 적용하며, 이를 우회하기 위해 CORS 정책이 필요하다.

동일 출처 정책(Same-Origin Policy)

브라우저가 보안상의 이유로 다른 도메인의 요청을 차단하는 보안 정책이다.
동일 출처(Same-Origin)의 기준은 프로토콜, 도메인, 포트가 모두 동일한 경우에만 적용된다.
예를 들어, https://example.com과 https://api.example.com은 다른 출처로 간주된다.
CORS 문제 발생 사례

클라이언트(React, Vue 등)와 백엔드(Spring Boot)가 다른 도메인에 있을 때, 브라우저는 기본적으로 요청을 차단한다.
예를 들어, React 프론트엔드(http://localhost:3000)에서 Spring Boot API(http://localhost:8080)에 데이터를 요청하면 CORS 에러가 발생한다.
Access to fetch at 'http://localhost:8080/api/data' from origin 'http://localhost:3000' has been blocked by CORS policy
이 오류를 해결하기 위해 서버에서 CORS 정책을 적절히 설정해야 한다.

CORS 해결 방법
CORS 정책을 설정하는 방법에는 여러 가지가 있으며, Spring Boot에서는 다양한 방식으로 적용할 수 있다.

Spring Boot에서 글로벌 CORS 설정
모든 API 요청에 대해 CORS를 허용하려면 Spring Boot의 CorsFilter를 설정해야 한다.
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.cors.CorsConfiguration;
import org.springframework.web.cors.UrlBasedCorsConfigurationSource;
import org.springframework.web.filter.CorsFilter;

import java.util.List;

@Configuration
public class CorsConfig {
    
    @Bean
    public CorsFilter corsFilter() {
        CorsConfiguration config = new CorsConfiguration();
        config.setAllowCredentials(true); // 쿠키 인증 요청 허용
        config.setAllowedOrigins(List.of("http://localhost:3000")); // 허용할 도메인 설정
        config.setAllowedMethods(List.of("GET", "POST", "PUT", "DELETE", "OPTIONS")); // 허용할 HTTP 메서드
        config.setAllowedHeaders(List.of("Authorization", "Cache-Control", "Content-Type")); // 허용할 헤더

        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
        source.registerCorsConfiguration("/**", config);

        return new CorsFilter(source);
    }
}
setAllowedOrigins(List.of("http://localhost:3000")): 특정 도메인에서만 요청을 허용하도록 설정.
setAllowCredentials(true): 쿠키와 인증 정보를 포함한 요청을 허용.
setAllowedMethods(List.of("GET", "POST", "PUT", "DELETE", "OPTIONS")): 사용할 HTTP 메서드 지정.
이 설정을 추가하면 http://localhost:3000에서 http://localhost:8080으로 요청을 보낼 수 있다.

Spring Security에서 CORS 설정
Spring Security를 사용하는 경우, Security 설정과 함께 CORS 정책을 적용해야 한다.
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .csrf().disable()
            .cors().and() // CORS 활성화
            .authorizeRequests()
            .antMatchers("/api/public/**").permitAll()
            .anyRequest().authenticated()
            .and()
            .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS);

        return http.build();
    }
}
cors().and()를 설정해야 Spring Security가 CORS 필터를 적용할 수 있다.
Spring Security와 함께 사용할 경우, CORS 설정이 제대로 적용되지 않는 문제가 발생할 수 있으므로 CorsFilter와 함께 사용해야 한다.
컨트롤러에서 개별 CORS 설정
특정 컨트롤러의 엔드포인트에 대해서만 CORS를 허용하고 싶다면 @CrossOrigin 어노테이션을 사용할 수 있다.
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api")
public class ExampleController {

    @CrossOrigin(origins = "http://localhost:3000")
    @GetMapping("/data")
    public String getData() {
        return "Hello, CORS!";
    }
}
@CrossOrigin(origins = "http://localhost:3000")
→ 특정 엔드포인트(/api/data)에 대해서만 http://localhost:3000에서 요청을 허용한다.

단점:

모든 엔드포인트에 대해 개별적으로 @CrossOrigin을 추가해야 하므로 관리가 어렵다.
CORS 적용 시 주의할 점
*(와일드카드) 사용 시 주의
setAllowedOrigins("*")로 설정하면 모든 도메인에서 API를 호출할 수 있지만,
Allow-Credentials가 true로 설정된 경우 *를 사용할 수 없다.
config.setAllowCredentials(true);
config.setAllowedOrigins(List.of("*")); // 오류 발생 가능
이 경우, 특정 도메인만 허용하는 방식으로 설정해야 한다.
OPTIONS 프리플라이트 요청 처리
POST, PUT, DELETE 같은 메서드는 사전 요청(preflight)을 필요로 한다.
사전 요청을 처리하지 않으면 클라이언트에서 CORS 오류가 발생할 수 있다.
Spring Boot에서는 OPTIONS 메서드를 허용해야 한다.
config.setAllowedMethods(List.of("GET", "POST", "PUT", "DELETE", "OPTIONS"));
Spring Security와 CORS 설정 충돌
Spring Security를 사용하면 CorsFilter보다 보안 필터가 먼저 적용될 수 있다.
해결 방법:
cors().and() 설정 추가.
CorsFilter를 명시적으로 등록.
실습 문제
문제 1: CORS 설정하기
아래 요구사항을 만족하는 코드를 작성하시오.

Spring Boot 애플리케이션에서 특정 도메인(https://example.com)에서만 API 요청을 허용하도록 설정한다.
GET, POST 메서드만 허용하도록 한다.
문제 2: 모든 도메인에서 API 요청을 허용하는 CORS 설정 추가
다음 요구사항을 만족하는 코드를 작성하시오.

모든 도메인에서 API 요청을 허용하도록 @CrossOrigin 애노테이션을 사용하여 설정한다.
PUT, DELETE 요청도 허용하도록 한다.
6. RESTful API 성능 최적화 기초
6.1. API 성능 최적화 개요
API 성능 최적화의 필요성
API 성능 최적화는 웹 애플리케이션의 응답 속도를 높이고 서버 부하를 줄이는 핵심 과정이다. RESTful API는 클라이언트-서버 구조로 동작하며, 클라이언트 요청을 빠르게 처리해야 사용자 경험(UX)이 개선되고 서버 리소스의 효율적 활용이 가능하다.

API 성능 최적화가 필요한 이유

빠른 응답 속도: API 응답이 지연되면 사용자의 이탈률이 증가한다.
서버 부하 감소: 불필요한 데이터 전송과 처리로 인해 서버 리소스가 낭비될 수 있다.
대량 요청 처리: 트래픽이 많은 경우 최적화되지 않은 API는 장애를 유발할 수 있다.
비용 절감: 서버의 부하를 줄이면 인프라 비용을 절감할 수 있다.
API 성능이 저하되는 원인

과도한 데이터 전송: 필요 이상의 데이터를 반환하면 네트워크와 클라이언트에서 불필요한 리소스를 소비한다.
잘못된 데이터베이스 쿼리: 비효율적인 SQL 쿼리로 인해 응답 시간이 증가할 수 있다.
N+1 문제 발생: 연관 데이터를 가져올 때, 쿼리가 과도하게 실행되면 성능이 저하된다.
불필요한 API 호출: 동일한 데이터를 반복적으로 요청하면 서버 부하가 증가한다.
캐싱 미활용: 정적인 데이터는 캐싱하면 성능이 크게 향상될 수 있다.
API 성능 최적화의 주요 전략
API 성능을 개선하기 위해 다음과 같은 전략을 사용할 수 있다.

응답 데이터 최적화

필요한 데이터만 응답하도록 필드를 제한한다.
JSON을 최소화하고, 불필요한 중첩을 제거한다.
쿼리 최적화

인덱스(Indexing) 를 활용하여 데이터베이스 조회 속도를 높인다.
N+1 문제 해결을 위해 JOIN을 활용하거나 페치 전략을 사용한다.
페이징(Paging)과 정렬(Sorting) 적용

대량의 데이터를 처리할 때는 페이징(Pagination) 을 적용하여 한 번에 불러오는 데이터를 제한한다.
정렬을 적용하여 필요한 데이터를 빠르게 조회할 수 있도록 한다.
캐싱(Caching) 활용

변경되지 않는 데이터는 캐싱(Cache) 을 적용하여 API 응답 속도를 높인다.
Redis, Memcached 같은 인메모리 데이터베이스를 활용한다.
비동기(Asynchronous) 처리

오래 걸리는 작업(파일 처리, 데이터 분석 등)은 비동기 API로 분리하여 성능을 개선한다.
압축(Compression) 적용

응답 데이터를 Gzip과 같은 압축 알고리즘으로 압축하여 네트워크 트래픽을 줄인다.
API 응답 최적화 예제
필요한 데이터만 반환하도록 DTO 사용
API에서 데이터를 반환할 때, 엔티티(Entity) 전체가 아닌 필요한 필드만 포함한 DTO(Data Transfer Object)를 활용한다.
public class UserDTO {
    private String username;
    private String email;

    public UserDTO(User user) {
        this.username = user.getUsername();
        this.email = user.getEmail();
    }

    // getter 생략
}
비효율적인 방식
User 엔티티 전체를 반환하여 불필요한 필드도 포함됨.
@GetMapping("/users")
public List<User> getUsers() {
    return userRepository.findAll();
}
최적화된 방식
DTO를 활용하여 필요한 데이터만 반환.
@GetMapping("/users")
public List<UserDTO> getUsers() {
    return userRepository.findAll().stream()
            .map(UserDTO::new)
            .collect(Collectors.toList());
}
쿼리 최적화 및 N+1 문제 해결
잘못된 쿼리는 여러 개의 추가적인 쿼리를 발생시키며, 이를 방지하기 위해 JOIN FETCH를 사용한다.
N+1 문제 발생 코드

@GetMapping("/users")
public List<User> getUsers() {
    return userRepository.findAll(); // 각 User에 대해 추가 쿼리 발생
}
해결 코드 (JOIN FETCH 사용)

@Query("SELECT u FROM User u JOIN FETCH u.orders")
List<User> findAllWithOrders();
페이징 적용
API에서 대량의 데이터를 처리할 때는 페이징을 적용하여 한 번에 많은 데이터를 불러오지 않도록 한다.
@GetMapping("/users")
public Page<User> getUsers(@PageableDefault(size = 10, sort = "id") Pageable pageable) {
    return userRepository.findAll(pageable);
}
size = 10: 한 번에 최대 10개의 데이터만 반환
sort = "id": 기본적으로 ID 기준으로 정렬
캐싱 적용
캐싱을 적용하여 같은 요청이 반복될 때 데이터베이스 호출을 줄일 수 있다.
@Cacheable("users")
@GetMapping("/users/{id}")
public User getUser(@PathVariable Long id) {
    return userRepository.findById(id).orElseThrow();
}
처음 요청: 데이터베이스에서 데이터를 조회하고 결과를 캐시에 저장.
이후 요청: 캐시에서 데이터를 반환하여 성능을 개선.
API 성능 최적화 적용 시 주의할 점
과도한 캐싱 사용

캐싱이 불필요한 경우, 최신 데이터가 반영되지 않을 수 있다.
사용자 정보와 같은 자주 변경되는 데이터는 캐싱하지 않는 것이 좋다.
잘못된 페이징 전략

데이터가 많을 경우, 무한 스크롤(Infinite Scrolling) 이나 Cursor 기반 페이징을 고려해야 한다.
OFFSET을 사용한 페이징은 데이터가 많아질수록 속도가 느려질 수 있다.
불필요한 JOIN 사용

무조건 JOIN FETCH를 사용하면 오히려 성능이 저하될 수 있다.
조회하는 데이터가 너무 많으면 Lazy Loading을 고려해야 한다.
학습자의 사고를 돕기 위한 질문
API 응답 속도를 저하시킬 수 있는 주요 요인은 무엇인가?

불필요한 데이터 로딩, 과도한 요청 처리, 비효율적인 데이터베이스 쿼리를 고려해보라.
API 성능을 개선하기 위한 일반적인 전략은 무엇인가?

캐싱, 페이징, 데이터 압축 등의 기법을 떠올려보라.
6.2. 캐싱을 활용한 성능 최적화
캐싱(Cache) 개념
캐싱(Cache)은 자주 사용되는 데이터나 요청 결과를 저장하여 성능을 향상시키는 기법이다. API에서는 동일한 요청이 반복될 경우 매번 데이터베이스를 조회하는 대신, 캐시에 저장된 데이터를 활용하여 성능을 최적화할 수 있다.

캐싱을 활용하면 다음과 같은 이점이 있다.

API 응답 속도 향상: 데이터베이스나 외부 API를 매번 호출하는 대신 캐시된 데이터를 반환하므로 응답 속도가 빠르다.
서버 부하 감소: 동일한 요청을 여러 번 처리하지 않으므로 불필요한 연산을 줄일 수 있다.
네트워크 트래픽 절감: 클라이언트가 동일한 데이터를 요청할 때 서버와의 통신을 최소화할 수 있다.
비용 절감: 클라우드 서비스에서 API 호출 비용이 절감될 수 있다.
캐싱은 클라이언트 측, 서버 측, 데이터베이스 측에서 모두 적용할 수 있으며, API 캐싱에서는 주로 서버 측 캐싱이 활용된다.

캐싱의 주요 유형
캐싱은 적용 위치와 방식에 따라 여러 유형으로 나뉜다.

클라이언트 측 캐싱(Client-Side Caching)

브라우저 또는 API 클라이언트가 데이터를 저장하여 재사용한다.
HTTP Cache-Control 헤더를 활용하여 캐싱을 설정할 수 있다.
서버 측 캐싱(Server-Side Caching)

API 서버가 요청 결과를 캐시에 저장하여 재사용한다.
주로 Redis, Memcached와 같은 인메모리 데이터베이스를 사용한다.
리버스 프록시 캐싱(Reverse Proxy Caching)

Nginx, Varnish 같은 프록시 서버가 API 응답을 캐싱하여 빠르게 제공한다.
트래픽이 많은 서비스에서 효과적이다.
데이터베이스 캐싱(Database Caching)

데이터베이스에서 자주 사용되는 쿼리 결과를 캐싱한다.
MySQL의 Query Cache 또는 Redis를 활용할 수 있다.
HTTP 캐싱을 활용한 API 최적화
HTTP 프로토콜은 캐싱을 지원하는 여러 헤더를 제공한다.

1. Cache-Control 헤더

HTTP 응답에서 Cache-Control을 설정하면 클라이언트나 프록시 서버가 응답을 캐싱할 수 있다.
Cache-Control: max-age=3600, public
max-age=3600: 3600초(1시간) 동안 캐싱 가능
public: 모든 사용자가 캐싱 가능
2. ETag(Entity Tag)

ETag는 리소스의 변경 여부를 판별하는 식별자 역할을 한다.
ETag: "abc123"
클라이언트는 If-None-Match 요청 헤더를 포함하여 변경 여부를 확인할 수 있다.
If-None-Match: "abc123"
서버에서 변경이 없으면 304 Not Modified 상태 코드로 응답하여 데이터를 다시 전송하지 않는다.
Spring Boot에서 캐싱 적용
Spring Boot에서는 @Cacheable, @CachePut, @CacheEvict 어노테이션을 사용하여 캐싱을 적용할 수 있다.

1. 캐싱 활성화

Spring Boot에서 캐싱을 사용하려면 @EnableCaching 어노테이션을 추가해야 한다.
@Configuration
@EnableCaching
public class CacheConfig {
}
2. @Cacheable을 사용한 캐싱 적용

@Cacheable을 사용하면 해당 메서드가 호출될 때 결과를 캐시에 저장하고, 이후 동일한 요청이 들어오면 캐시된 데이터를 반환한다.
@Cacheable("users")
@GetMapping("/users/{id}")
public User getUser(@PathVariable Long id) {
    return userRepository.findById(id).orElseThrow();
}
@Cacheable("users"):
users라는 캐시 공간에 데이터를 저장한다.
같은 요청이 들어오면 캐시된 데이터를 반환한다.
새로운 데이터가 추가되면 캐시가 자동으로 갱신되지 않는다.
3. @CachePut을 사용하여 캐시 업데이트

@CachePut을 사용하면 데이터를 변경할 때 캐시도 업데이트된다.
@CachePut(value = "users", key = "#user.id")
@PutMapping("/users/{id}")
public User updateUser(@PathVariable Long id, @RequestBody User user) {
    user.setId(id);
    return userRepository.save(user);
}
@CachePut(value = "users", key = "#user.id"):
사용자가 업데이트될 때 해당 ID의 캐시 데이터도 갱신된다.
4. @CacheEvict을 사용하여 캐시 삭제

@CacheEvict을 사용하면 특정 데이터가 삭제될 때 캐시도 함께 제거된다.
@CacheEvict(value = "users", key = "#id")
@DeleteMapping("/users/{id}")
public void deleteUser(@PathVariable Long id) {
    userRepository.deleteById(id);
}
@CacheEvict(value = "users", key = "#id"):
사용자가 삭제될 때 해당 ID의 캐시도 제거된다.
Redis를 활용한 캐싱 적용
Spring Boot에서 Redis를 활용하여 캐싱을 적용할 수도 있다.

1. Redis 설정 추가

spring-boot-starter-data-redis 의존성을 추가한다.
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
2. Redis 설정 파일 작성

Redis 캐시를 사용하려면 RedisTemplate을 설정해야 한다.
@Configuration
public class RedisConfig {

    @Bean
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory connectionFactory) {
        RedisTemplate<String, Object> template = new RedisTemplate<>();
        template.setConnectionFactory(connectionFactory);
        return template;
    }
}
3. 캐싱 적용

기존의 @Cacheable 어노테이션을 사용하여 Redis에 캐시 데이터를 저장할 수 있다.
@Cacheable(value = "users", key = "#id")
@GetMapping("/users/{id}")
public User getUser(@PathVariable Long id) {
    return userRepository.findById(id).orElseThrow();
}
4. Redis에서 캐시 조회

Redis CLI를 통해 캐싱된 데이터를 확인할 수 있다.
redis-cli
keys *
캐싱 적용 시 주의할 점
과도한 캐싱 사용

모든 API에 캐싱을 적용하는 것은 비효율적일 수 있다.
자주 변경되는 데이터(사용자 정보, 주문 상태 등) 는 캐싱하면 데이터 불일치 문제가 발생할 수 있다.
TTL(Time-To-Live) 설정

캐시가 너무 오래 유지되면 오래된 데이터가 반환될 수 있다.
@Cacheable을 사용할 때는 TTL을 설정하여 캐시된 데이터를 적절한 주기로 갱신해야 한다.
캐시 일관성 유지

데이터가 변경될 때 캐시도 함께 갱신되도록 @CachePut과 @CacheEvict을 적절히 사용해야 한다.
6.3. 데이터 페이징 및 정렬
데이터 페이징(Paging) 개념
대규모 데이터를 처리하는 API에서는 한 번에 모든 데이터를 반환하는 방식이 비효율적이다.
이러한 문제를 해결하기 위해 페이징(Paging) 기법을 사용한다.

페이징이 필요한 주요 이유는 다음과 같다.

응답 속도 개선: 필요한 데이터만 반환하므로 API 응답 시간이 단축된다.
서버 부하 감소: 불필요한 데이터 전송을 줄여 서버의 부하를 줄일 수 있다.
네트워크 트래픽 절감: 클라이언트가 필요한 데이터만 요청하므로 불필요한 데이터 전송이 방지된다.
사용자 경험 개선: 페이지 단위로 데이터를 제공하면 UI에서 보다 효율적으로 데이터를 로드할 수 있다.
페이징 기법을 활용하면 데이터의 특정 부분을 선택적으로 반환할 수 있으며, 일반적으로 오프셋 기반 페이징(Offset Pagination) 과 커서 기반 페이징(Cursor Pagination) 이 사용된다.

오프셋 기반 페이징(Offset Pagination)
오프셋 기반 페이징은 페이지 번호와 개수를 기준으로 데이터의 특정 부분을 조회하는 방식이다.

쿼리 매개변수 예시:

GET /users?page=2&size=10
위와 같은 요청이 들어오면, page=2는 두 번째 페이지를 의미하며, size=10은 한 페이지당 10개의 데이터를 반환하도록 설정하는 것이다.

SQL에서 OFFSET과 LIMIT을 사용하여 이를 구현할 수 있다.

SELECT * FROM users
ORDER BY id ASC
LIMIT 10 OFFSET 10;
LIMIT 10: 한 번에 10개만 반환
OFFSET 10: 10개를 건너뛴 후 데이터 조회 (즉, 2번째 페이지)
이 방식은 구현이 간단하지만, 데이터가 많아질수록 성능이 저하되는 문제가 있다.
특히, 높은 오프셋 값을 사용할 경우, 불필요한 레코드 검색 비용이 증가할 수 있다.

커서 기반 페이징(Cursor Pagination)
커서 기반 페이징은 특정 데이터(예: ID)를 기준으로 다음 데이터를 조회하는 방식이다.
오프셋 기반 페이징보다 성능이 우수하며, 대량 데이터를 처리하는 API에서 선호된다.

쿼리 매개변수 예시:

GET /users?cursor=50&size=10
위 요청은 id 값이 50 이상인 10개의 데이터를 가져오도록 한다.

SQL에서는 WHERE 조건을 활용하여 구현할 수 있다.

SELECT * FROM users
WHERE id > 50
ORDER BY id ASC
LIMIT 10;
id > 50: ID가 50보다 큰 데이터만 조회
LIMIT 10: 최대 10개의 데이터 반환
커서 기반 페이징은 데이터 삭제 및 추가가 발생해도 페이징의 무결성을 유지할 수 있다는 장점이 있다.
단, ID 값을 기준으로 정렬해야 하며, 단순한 페이지 이동이 어렵다는 단점이 있다.

Spring Data JPA를 활용한 페이징
Spring Boot에서는 Spring Data JPA의 Pageable 인터페이스를 사용하여 페이징을 쉽게 구현할 수 있다.

1. Repository에서 Pageable을 적용한 페이징 메서드 정의

@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    Page<User> findAll(Pageable pageable);
}
2. Controller에서 페이징을 적용한 API 구현

@RestController
@RequestMapping("/users")
public class UserController {

    @Autowired
    private UserRepository userRepository;

    @GetMapping
    public Page<User> getUsers(@RequestParam(defaultValue = "0") int page,
                               @RequestParam(defaultValue = "10") int size) {
        Pageable pageable = PageRequest.of(page, size, Sort.by("id").ascending());
        return userRepository.findAll(pageable);
    }
}
PageRequest.of(page, size, Sort.by("id").ascending())
page: 페이지 번호 (0부터 시작)
size: 한 페이지에 포함할 데이터 개수
Sort.by("id").ascending(): ID 기준 오름차순 정렬
3. API 요청 예시

GET /users?page=1&size=5
4. JSON 응답 예시

{
    "content": [
        {"id": 6, "name": "Alice"},
        {"id": 7, "name": "Bob"},
        {"id": 8, "name": "Charlie"},
        {"id": 9, "name": "David"},
        {"id": 10, "name": "Eve"}
    ],
    "totalElements": 50,
    "totalPages": 10,
    "size": 5,
    "number": 1
}
content: 실제 데이터 목록
totalElements: 전체 데이터 개수
totalPages: 총 페이지 개수
size: 한 페이지당 개수
number: 현재 페이지 번호
정렬(Sorting) 개념
페이징과 함께 데이터 정렬(Sorting) 을 적용하면 더욱 효율적인 API 설계가 가능하다.
정렬은 일반적으로 오름차순(ASC) 또는 내림차순(DESC) 방식으로 데이터를 정렬하는 것이다.

쿼리 매개변수 예시:

GET /users?page=0&size=5&sort=name,asc
Spring Data JPA에서 정렬을 적용하는 방법은 다음과 같다.

@GetMapping
public Page<User> getUsers(@RequestParam(defaultValue = "0") int page,
                           @RequestParam(defaultValue = "10") int size,
                           @RequestParam(defaultValue = "id,asc") String sort) {
    String[] sortParams = sort.split(",");
    Sort.Direction direction = Sort.Direction.fromString(sortParams[1]);
    Pageable pageable = PageRequest.of(page, size, Sort.by(direction, sortParams[0]));
    return userRepository.findAll(pageable);
}
sort=name,asc → name을 기준으로 오름차순 정렬
sort=createdAt,desc → createdAt을 기준으로 내림차순 정렬
이렇게 하면 사용자가 원하는 기준으로 동적으로 정렬할 수 있는 API가 된다.

페이징과 정렬 적용 시 주의할 점
데이터 정합성 유지

페이징 처리 시, 데이터가 변경되면 페이지 간의 불일치 문제가 발생할 수 있음 (예: 한 페이지에서 조회한 데이터가 삭제되면 다음 페이지의 데이터가 이동됨)
createdAt 또는 id를 기준으로 정렬하여 정합성을 유지하는 것이 중요함
대량 데이터에서 OFFSET 사용 주의

오프셋(Offset) 값이 클 경우, 데이터베이스의 검색 비용이 증가함
WHERE id > ? 형태의 커서 기반 페이징을 적용하는 것이 성능상 유리함
동적 정렬 시 SQL Injection 방지

사용자가 임의의 컬럼명을 입력하여 SQL Injection 공격을 수행할 수 있음
정렬 기준을 미리 정의하고 검증하는 방식이 필요함
6.4. API 요청 수 줄이기
API 요청 수를 줄여야 하는 이유
RESTful API를 설계할 때, 클라이언트가 서버에 보내는 요청 수를 줄이는 것은 매우 중요하다.
불필요한 요청이 많아지면 다음과 같은 문제가 발생할 수 있다.

서버 부하 증가

클라이언트가 과도하게 많은 요청을 보내면 서버의 부하가 증가하고 응답 속도가 느려진다.
네트워크 비용 증가

요청이 많을수록 네트워크 트래픽이 증가하고, 이는 클라이언트와 서버 모두에 부담을 준다.
사용자 경험 악화

사용자가 데이터를 요청할 때마다 기다려야 한다면, 서비스의 품질이 낮아진다.
따라서 API 요청을 최소화하는 다양한 기법을 활용하여 API의 성능을 최적화하는 것이 중요하다.

N+1 문제 해결
N+1 문제는 API에서 여러 개의 관련된 데이터를 조회할 때 발생하는 성능 저하 문제이다.
예를 들어, 다음과 같은 관계를 가진 데이터가 있다고 가정하자.

User 엔티티가 Order 엔티티와 1:N 관계를 맺고 있음
특정 사용자의 주문 목록을 조회하는 API를 호출한다고 가정
잘못된 방식 (N+1 문제 발생)

@GetMapping("/users/{id}/orders")
public List<Order> getUserOrders(@PathVariable Long id) {
    User user = userRepository.findById(id).orElseThrow();
    return user.getOrders(); // 각 주문을 조회할 때 추가적인 쿼리 실행
}
이 방식은 다음과 같은 문제가 발생한다.

userRepository.findById(id) 실행 (1개의 쿼리)
user.getOrders() 실행 시 각 주문마다 추가적인 조회 (N개의 쿼리)
즉, 총 1 + N 개의 쿼리가 실행되며, 데이터가 많을수록 성능이 급격히 저하된다.

해결 방법: join fetch 활용

@GetMapping("/users/{id}/orders")
public List<Order> getUserOrders(@PathVariable Long id) {
    return orderRepository.findOrdersByUserId(id);
}
@Repository
public interface OrderRepository extends JpaRepository<Order, Long> {
    @Query("SELECT o FROM Order o JOIN FETCH o.user WHERE o.user.id = :userId")
    List<Order> findOrdersByUserId(@Param("userId") Long userId);
}
이렇게 하면 한 번의 쿼리만으로 사용자와 주문 목록을 동시에 조회할 수 있다.

데이터 압축 적용 (Gzip 사용)
RESTful API 응답 크기를 줄이기 위해 Gzip 압축을 활용할 수 있다.
Gzip을 사용하면 텍스트 기반 응답(JSON, XML 등)의 크기를 70~90%까지 감소시킬 수 있다.

Spring Boot에서 Gzip 활성화 방법

server:
  compression:
    enabled: true
    mime-types: application/json,application/xml,text/plain
    min-response-size: 1024
enabled: true: Gzip 압축을 활성화
mime-types: 압축할 콘텐츠 유형 설정
min-response-size: 1KB 이상의 응답만 압축
이 설정을 적용하면, 클라이언트가 요청할 때 Gzip을 지원하면 자동으로 응답이 압축된다.

데이터 필터링 및 최소화
API 응답에서 불필요한 필드가 포함되면 네트워크 트래픽이 증가하고, 클라이언트에서 처리해야 할 데이터가 많아진다.
이를 방지하기 위해 필요한 데이터만 반환하는 방식을 적용해야 한다.

잘못된 방식 (불필요한 데이터 포함)

{
  "id": 1,
  "name": "John Doe",
  "email": "johndoe@example.com",
  "password": "hashed_password",
  "createdAt": "2024-03-10T10:00:00",
  "updatedAt": "2024-03-11T12:00:00"
}
위 JSON 응답에서 password, createdAt, updatedAt 같은 불필요한 데이터가 포함되어 있다.

해결 방법: DTO(Data Transfer Object) 사용

public class UserDTO {
    private Long id;
    private String name;
    private String email;

    public UserDTO(User user) {
        this.id = user.getId();
        this.name = user.getName();
        this.email = user.getEmail();
    }
}
@GetMapping("/users/{id}")
public UserDTO getUser(@PathVariable Long id) {
    User user = userRepository.findById(id).orElseThrow();
    return new UserDTO(user);
}
이렇게 하면, 클라이언트가 필요로 하는 데이터만 반환할 수 있다.

API 응답 캐싱 (ETag, Last-Modified 활용)
API 요청을 줄이는 또 다른 효과적인 방법은 캐싱(Cache) 을 활용하는 것이다.
HTTP 캐싱을 적용하면, 동일한 요청이 반복될 경우 서버가 데이터를 다시 제공하지 않고, 클라이언트가 캐시된 데이터를 사용할 수 있다.

1. ETag(엔터티 태그)

ETag는 리소스의 변경 여부를 확인하는 해시값 역할을 한다.
클라이언트가 If-None-Match 헤더를 사용하여 변경 여부를 서버에 확인하면, 변경되지 않은 경우 304 응답을 받을 수 있다.
Spring Boot에서 ETag 적용

@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public ResponseEntity<UserDTO> getUser(@PathVariable Long id,
                                           @RequestHeader(value = "If-None-Match", required = false) String ifNoneMatch) {
        User user = userRepository.findById(id).orElseThrow();
        String etag = generateETag(user);

        if (etag.equals(ifNoneMatch)) {
            return ResponseEntity.status(HttpStatus.NOT_MODIFIED).build();
        }

        return ResponseEntity.ok()
                .header(HttpHeaders.ETAG, etag)
                .body(new UserDTO(user));
    }

    private String generateETag(User user) {
        return "\"" + user.getUpdatedAt().hashCode() + "\"";
    }
}
If-None-Match 헤더를 사용하여 ETag 값을 비교
변경되지 않았다면 304 Not Modified를 반환하여 요청을 줄임
2. Last-Modified 헤더 활용

특정 데이터가 변경된 시간을 기반으로 클라이언트가 최신 데이터인지 확인할 수 있다.
@GetMapping("/{id}")
public ResponseEntity<UserDTO> getUser(@PathVariable Long id,
                                       @RequestHeader(value = "If-Modified-Since", required = false) String ifModifiedSince) {
    User user = userRepository.findById(id).orElseThrow();
    long lastModified = user.getUpdatedAt().getTime();

    if (ifModifiedSince != null && lastModified <= Long.parseLong(ifModifiedSince)) {
        return ResponseEntity.status(HttpStatus.NOT_MODIFIED).build();
    }

    return ResponseEntity.ok()
            .lastModified(lastModified)
            .body(new UserDTO(user));
}
클라이언트가 If-Modified-Since 헤더를 보내면 변경 여부를 판단하여 304 응답 반환 가능
7. RESTful API 문서화
7.1. API 문서화 개요
API 문서화의 필요성
RESTful API를 개발할 때, 문서화(Documenting) 는 필수적인 과정이다.
API 문서화가 중요한 이유는 다음과 같다.

개발자 간 원활한 협업

API를 사용하는 프론트엔드, 모바일 개발자 또는 외부 파트너가 API의 사용법을 쉽게 이해할 수 있다.
API 유지보수 용이

API가 변경될 때마다 문서를 최신 상태로 유지하면, API의 관리가 쉬워진다.
일관성 있는 API 설계 가능

명확한 문서를 작성하면 API 설계의 일관성을 유지하는 데 도움을 준다.
외부 개발자 및 파트너 지원

API가 외부 개발자에게 공개되는 경우, 명확한 문서가 API 사용의 핵심 요소가 된다.
API 문서화 방식 비교
API 문서를 작성하는 방법은 크게 자동 문서화와 수동 문서화로 나뉜다.

문서화 방식	설명	장점	단점
자동 문서화	코드 기반으로 API 문서를 자동 생성	문서 관리 부담이 적음	코드와 문서가 불일치할 가능성
수동 문서화	Markdown 또는 외부 문서화 도구 사용	문서의 자유도가 높음	지속적인 관리가 필요
자동 문서화는 Swagger(OpenAPI) , Spring REST Docs 같은 도구를 사용하며,
수동 문서화는 Markdown, Confluence, Notion 등의 도구를 활용한다.

API 문서화 시 포함해야 할 요소
RESTful API 문서를 작성할 때는 다음과 같은 정보가 포함되어야 한다.

API 설명

API의 목적과 기능 설명
예: "이 API는 사용자의 정보를 조회하는 기능을 제공합니다."
엔드포인트 정보

API의 URL, HTTP 메서드, 요청 예제
GET /users/{id}
요청 파라미터 및 본문

필수 파라미터 및 선택적 파라미터 설명
{
  "name": "John Doe",
  "email": "johndoe@example.com"
}
응답 형식

응답 데이터 예시 제공
{
  "id": 1,
  "name": "John Doe",
  "email": "johndoe@example.com"
}
HTTP 상태 코드

성공 및 에러 응답 코드 정의
200 OK - 성공
400 Bad Request - 요청 오류
404 Not Found - 리소스를 찾을 수 없음
API 문서화의 핵심 원칙
RESTful API 문서화는 단순히 문서를 작성하는 것이 아니라 사용하기 쉬운 문서를 제공해야 한다.
이를 위해 다음과 같은 원칙을 고려해야 한다.

일관된 문서 스타일 유지

API 문서의 레이아웃과 구조를 통일성 있게 유지해야 한다.
예제 코드 제공

API 사용법을 쉽게 이해할 수 있도록, 요청 및 응답 예제 코드를 제공해야 한다.
자동화된 문서화 활용

Swagger 또는 Spring REST Docs를 사용하여, 문서의 최신 상태를 유지하도록 한다.
버전 관리를 통한 문서 업데이트

API가 변경될 경우, 문서도 함께 업데이트해야 한다.
학습자의 사고를 돕기 위한 질문
API 문서화가 중요한 이유는 무엇인가?

API를 사용하는 개발자들이 정확한 정보를 얻기 위해 어떤 점이 필요한지 생각해보라.
자동화된 API 문서화와 수동 API 문서화의 차이는 무엇인가?

유지보수성과 정확성 측면에서 각각의 장단점을 고려해보라.
7.2. Swagger(OpenAPI) 활용
Swagger란 무엇인가?
Swagger는 OpenAPI Specification(OAS) 을 기반으로 API를 문서화하는 도구다.
이전에는 Swagger라는 이름으로 불렸지만, 현재는 OpenAPI라는 공식 명칭이 사용된다.
Swagger를 사용하면 API의 명세를 자동으로 생성하고, UI를 통해 API를 테스트할 수도 있다.

Swagger(OpenAPI)의 주요 기능은 다음과 같다.

API 자동 문서화

애플리케이션 코드에서 API 문서를 자동으로 생성한다.
직관적인 UI 제공

Swagger UI를 통해 API의 요청 및 응답을 쉽게 테스트할 수 있다.
API 정의의 표준화

OpenAPI 명세를 기반으로 일관된 API 문서를 제공한다.
다양한 언어 및 프레임워크 지원

Java(Spring Boot), Node.js, Python(FastAPI) 등 다양한 언어에서 사용할 수 있다.
Swagger를 사용해야 하는 이유
API 문서화는 필수적이지만, 수동으로 문서를 관리하면 유지보수가 어렵다.
Swagger를 사용하면 API가 변경될 때마다 자동으로 최신 문서를 생성할 수 있어 관리가 편리하다.

Swagger를 도입하면 다음과 같은 장점이 있다.

API 문서 자동 업데이트:

코드 기반의 문서화로 API가 변경될 때마다 자동으로 반영된다.
API 테스트 환경 제공:

개발자와 QA 엔지니어가 별도의 도구 없이 API를 테스트할 수 있다.
개발자 경험(Developer Experience, DX) 향상:

API를 사용하는 외부 개발자가 쉽게 API를 이해하고 활용할 수 있다.
Swagger UI의 기본 개념
Swagger는 Swagger UI라는 웹 기반 인터페이스를 제공한다.
Swagger UI는 API 명세를 시각적으로 보여주며, 개발자가 직접 API 요청을 테스트할 수 있도록 돕는다.

Swagger UI를 사용하면 다음과 같은 기능을 수행할 수 있다.

API의 엔드포인트 목록 확인

모든 API 엔드포인트가 자동으로 문서화된다.
각 API의 요청 및 응답 형식 확인

요청 파라미터, 응답 데이터 형식 등을 시각적으로 확인할 수 있다.
API 호출 테스트 기능

직접 API 요청을 실행하고, 응답을 즉시 확인할 수 있다.
Spring Boot에서 Swagger 설정 방법
Spring Boot에서 Swagger를 사용하려면 springdoc-openapi 라이브러리를 추가해야 한다.
Spring Boot 3.x 버전 이후에는 springdoc-openapi를 공식적으로 지원하며, 설정도 간단하다.

의존성 추가

pom.xml 파일에 springdoc-openapi 라이브러리를 추가한다.

<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.1.0</version>
</dependency>
Swagger UI 활성화

springdoc-openapi를 추가하면 기본적으로 /swagger-ui.html 경로에서 Swagger UI를 사용할 수 있다.
별도의 설정 없이 API 문서를 자동으로 생성할 수 있다.

Swagger UI 기본 URL:
http://localhost:8080/swagger-ui.html
Swagger 설정 커스터마이징

기본 설정을 변경하고 싶다면, application.properties에 다음과 같이 설정할 수 있다.

# Swagger 문서의 기본 경로 설정
springdoc.api-docs.path=/api-docs

# Swagger UI 경로 설정
springdoc.swagger-ui.path=/swagger-ui
API 문서 커스터마이징

특정 컨트롤러나 API 엔드포인트에 설명을 추가하려면 @Operation 및 @Parameter 애너테이션을 사용할 수 있다.

import io.swagger.v3.oas.annotations.Operation;
import io.swagger.v3.oas.annotations.Parameter;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/users")
public class UserController {

    @Operation(summary = "사용자 조회", description = "사용자의 정보를 조회합니다.")
    @GetMapping("/{id}")
    public String getUser(
        @Parameter(description = "조회할 사용자의 ID") @PathVariable Long id) {
        return "User ID: " + id;
    }
}
위와 같이 작성하면 Swagger UI에서 API 설명이 자동으로 표시된다.

Swagger API 문서 예제
Swagger를 사용하면 다음과 같은 API 문서를 자동으로 생성할 수 있다.

Swagger UI 예제

GET /users/{id}
- 설명: 사용자 정보를 조회합니다.
- 요청 파라미터: id (Long)
- 응답 예시:
{
    "id": 1,
    "name": "John Doe",
    "email": "johndoe@example.com"
}
Swagger UI 화면 예시

http://localhost:8080/swagger-ui.html에 접속하면 API 목록과 상세 정보를 확인할 수 있다.
Swagger 적용 시 주의할 점
Swagger는 강력한 도구이지만, 실제 운영 환경에서는 몇 가지 주의해야 할 사항이 있다.

보안 설정 필요

Swagger UI는 기본적으로 모든 API를 노출하므로, 운영 환경에서는 접근을 제한해야 한다.
불필요한 API 문서화 방지

내부 전용 API까지 Swagger에 노출되면 보안상 문제가 될 수 있다.

@Hidden 애너테이션을 사용하여 특정 API를 Swagger에서 제외할 수 있다.

import io.swagger.v3.oas.annotations.Hidden;

@Hidden
@RestController
@RequestMapping("/internal")
public class InternalController {
    @GetMapping("/data")
    public String getInternalData() {
        return "Internal Data";
    }
}
응답 데이터의 명확한 정의 필요

API 응답 데이터 형식을 명확하게 정의하지 않으면, Swagger 문서가 혼란스러울 수 있다.
@Schema 애너테이션을 활용하여 데이터 모델을 명확히 정의하는 것이 좋다.
Swagger를 통한 API 문서화 흐름
Swagger를 활용한 API 문서화의 일반적인 흐름은 다음과 같다.

springdoc-openapi 추가 → Swagger UI 자동 활성화
@Operation 및 @Parameter 애너테이션 추가 → API 설명 추가
Swagger UI에서 API 동작 확인 및 테스트 → API 동작 검증
운영 환경에서 Swagger 접근 제한 설정 → 보안 강화
7.3. Spring REST Docs 활용
Spring REST Docs란?
Spring REST Docs는 테스트 기반의 REST API 문서화 도구다.
Swagger(OpenAPI)와 달리, API의 실제 동작을 기반으로 문서를 자동 생성한다.

Spring REST Docs의 특징은 다음과 같다.

테스트 기반 문서화

API 테스트 코드 실행 결과를 기반으로 문서를 자동 생성한다.
정확한 문서 제공

API의 실제 응답과 요청을 바탕으로 문서가 생성되므로,
API 변경이 있을 경우 자동으로 문서가 업데이트된다.
Markdown 및 Asciidoc 지원

Spring REST Docs는 기본적으로 Asciidoc을 지원하며,
이를 HTML 문서로 변환하여 제공할 수 있다.
Swagger와의 차이점

Swagger는 코드 기반으로 문서를 생성하는 반면,
Spring REST Docs는 API 테스트 결과를 기반으로 문서를 생성한다.
Spring REST Docs를 사용해야 하는 이유
Spring REST Docs는 API 변경이 발생해도 테스트 코드를 유지하는 한 문서가 정확하게 관리된다.
이는 문서와 실제 API 구현 간 불일치를 방지하는 데 큰 도움이 된다.

Spring REST Docs를 사용하면 다음과 같은 장점이 있다.

자동 문서 업데이트:

API의 변경 사항이 반영된 테스트를 실행하면 문서도 자동으로 변경된다.
API 문서의 신뢰성 보장:

실제 요청 및 응답을 기반으로 문서가 생성되므로 문서와 코드 간 불일치 문제가 발생하지 않는다.
일반 Markdown 또는 Asciidoc 형식 지원:

개발자가 원하는 포맷으로 문서를 구성할 수 있다.
Spring REST Docs 설정 방법
Spring REST Docs를 사용하려면 다음과 같은 설정이 필요하다.

의존성 추가

pom.xml에 Spring REST Docs 관련 의존성을 추가한다.

<dependency>
    <groupId>org.springframework.restdocs</groupId>
    <artifactId>spring-restdocs-mockmvc</artifactId>
    <version>3.0.0</version>
    <scope>test</scope>
</dependency>
테스트 코드에서 REST Docs 설정

Spring Boot에서는 MockMvc와 함께 REST Docs를 설정할 수 있다.

import static org.springframework.restdocs.mockmvc.MockMvcRestDocumentation.document;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultHandlers.print;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.restdocs.mockmvc.RestDocumentationRequestBuilders;
import org.springframework.restdocs.mockmvc.RestDocumentationResultHandler;
import org.springframework.restdocs.mockmvc.MockMvcRestDocumentation;
import org.springframework.restdocs.operation.preprocess.Preprocessors;

@WebMvcTest
public class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    private RestDocumentationResultHandler documentationHandler;

    @BeforeEach
    public void setUp() {
        documentationHandler = MockMvcRestDocumentation.document(
                "{class-name}/{method-name}",
                Preprocessors.preprocessRequest(Preprocessors.prettyPrint()),
                Preprocessors.preprocessResponse(Preprocessors.prettyPrint())
        );
    }

    @Test
    public void getUser() throws Exception {
        mockMvc.perform(get("/users/1"))
            .andExpect(status().isOk())
            .andDo(print())
            .andDo(documentationHandler);
    }
}
위 테스트를 실행하면 실제 API 응답 결과를 기반으로 문서가 자동 생성된다.

Spring REST Docs의 문서 생성 방식
Spring REST Docs는 @AutoConfigureRestDocs 또는 MockMvc 설정을 통해 API 응답 데이터를 기반으로
자동 문서를 생성하는 방식이다.

문서의 주요 구성 요소는 다음과 같다.

요청(Request)

API 호출에 필요한 HTTP 메서드, 요청 URL, 요청 파라미터 등의 정보
응답(Response)

API 호출 결과로 반환되는 응답 본문(JSON), HTTP 상태 코드, 응답 헤더 등의 정보
예제(Example)

실제 API 호출 시의 요청 및 응답 예제 제공
Spring REST Docs로 생성된 문서 예제
테스트 코드 실행 후 생성된 API 문서의 예제는 다음과 같다.

==== 사용자 조회 API
* 요청 방식: GET /users/{id}
* 요청 예시:
  - 요청 URL: /users/1
  - 요청 파라미터: id (Long)
* 응답 예시:
  {
      "id": 1,
      "name": "John Doe",
      "email": "johndoe@example.com"
  }
위 문서는 Asciidoc 형식으로 변환될 수 있으며, HTML로도 제공할 수 있다.

Spring REST Docs 적용 시 고려할 사항
테스트 코드 유지보수 필요

API가 변경되면 테스트 코드도 수정해야 하므로, Swagger보다 유지보수 비용이 들 수 있다.
Swagger와의 차이점 고려

Spring REST Docs는 문서를 따로 확인해야 하지만,
Swagger는 UI에서 즉시 API를 호출할 수 있다는 장점이 있다.
운영 환경에서는 문서 공개 범위 설정 필요

개발 환경에서는 문서를 자유롭게 열람할 수 있도록 하지만,
운영 환경에서는 내부 문서만 접근 가능하도록 설정하는 것이 필요하다.
Spring REST Docs와 Swagger 비교
비교 항목	Swagger(OpenAPI)	Spring REST Docs
문서 생성 방식	코드 기반	테스트 기반
UI 제공 여부	Swagger UI 제공	제공하지 않음
API 테스트 기능	Swagger UI에서 가능	불가능
유지보수 편리성	API 변경 시 자동 반영	테스트 코드 수정 필요
문서 신뢰성	수동 작성 시 오류 가능	실제 응답 기반으로 신뢰성 높음
Spring REST Docs를 통한 API 문서화 흐름
Spring REST Docs를 사용한 API 문서화 과정은 다음과 같다.

테스트 코드 작성 및 실행

MockMvc를 활용하여 API 호출을 테스트한다.
API 응답 결과 기반 문서 자동 생성

요청 및 응답 데이터를 바탕으로 문서가 생성된다.
Markdown, Asciidoc 형식으로 변환

개발자가 원하는 문서 포맷으로 변환 가능하다.
문서 배포 및 활용

생성된 문서를 HTML로 변환하여 API 문서로 제공할 수 있다.
연습 문제
문제 1: RESTful API 엔드포인트 설계
RESTful API를 설계할 때 엔드포인트 URL은 명사(Noun) 기반으로 정의해야 한다. 아래의 기능을 수행하는 API 엔드포인트를 설계하시오.

전체 도서 목록을 조회하는 API 엔드포인트를 정의하시오.
특정 도서(bookId) 정보를 조회하는 API 엔드포인트를 정의하시오.
새로운 도서를 추가하는 API 엔드포인트를 정의하시오.
특정 도서의 정보를 수정하는 API 엔드포인트를 정의하시오.
특정 도서를 삭제하는 API 엔드포인트를 정의하시오.
요구사항:

엔드포인트는 RESTful 규칙을 따라야 한다.
적절한 HTTP 메서드를 사용해야 한다.
문제 2: HTTP 상태 코드 매칭
아래 시나리오에서 적절한 HTTP 상태 코드를 매칭하시오.

클라이언트가 존재하지 않는 bookId로 도서를 조회했을 때.
새로운 도서가 정상적으로 추가되었을 때.
클라이언트가 필수 데이터 없이 요청을 보냈을 때.
서버에서 처리 중 예기치 않은 오류가 발생했을 때.
인증되지 않은 사용자가 도서를 삭제하려고 할 때.
요구사항:

각 시나리오에 맞는 정확한 HTTP 상태 코드를 반환해야 한다.
상태 코드의 의미를 고려하여 선택해야 한다.
문제 3: 표준화된 오류 응답 설계
RESTful API의 오류 응답은 일관된 구조를 가져야 한다. 다음 요구사항을 만족하는 JSON 오류 응답을 설계하시오.

상태 코드: 403 Forbidden
오류 메시지: "접근 권한이 없습니다."
오류 코드: "ERR_403"
요청한 타임스탬프 포함.
요구사항:

오류 응답은 JSON 형식으로 구성해야 한다.
응답에 포함될 필드는 status, error, message, code, timestamp 여야 한다.
문제 4: HATEOAS 적용
HATEOAS를 적용하여 API 응답에 링크를 포함하는 JSON 응답을 설계하시오.

주문 ID: 202501
상태: "PROCESSING"
다음과 같은 링크를 포함:
self: 현재 주문 상세 조회 (/orders/202501)
cancel: 주문 취소 (/orders/202501/cancel), 단 PROCESSING 상태일 경우만 표시
next: 다음 주문 조회 (/orders/202502)
요구사항:

링크 정보는 links 배열에 포함되어야 한다.
주문 상태에 따라 cancel 링크가 동적으로 포함되도록 설계해야 한다.
문제 5: CORS 설정 추가
Spring Boot에서 특정 도메인(https://client-app.com)에서만 GET, POST 요청을 허용하는 CORS 설정을 추가하는 코드를 작성하시오.

요구사항:

특정 도메인에서만 요청을 허용해야 한다.
GET, POST 요청만 허용해야 한다.
Spring Boot의 CorsRegistry를 사용해야 한다.
문제 6: RESTful API의 상태 변화 처리
주문(Order) 상태를 업데이트하는 API 엔드포인트를 설계하시오.

주문 ID 9876의 상태를 "DELIVERED"로 변경하는 API 엔드포인트를 정의하시오.
PUT 또는 PATCH 중 적절한 HTTP 메서드를 선택하여 사용하시오.
요청 본문(Request Body) 형식을 정의하시오.
요구사항:

상태 변경이 필요한 경우 PUT과 PATCH 중 적절한 HTTP 메서드를 사용해야 한다.
상태 업데이트 요청은 JSON 형식의 본문을 포함해야 한다.
문제 7: RESTful API 버전 관리
다음 RESTful API를 버전별로 관리하는 방법을 설계하시오.

URL 기반 버전 관리 방식(/v1, /v2 활용)
요청 헤더 기반 버전 관리 방식(Accept: application/vnd.api.v1+json 활용)
요구사항:

API 버전이 포함된 엔드포인트를 정의해야 한다.
요청 헤더 기반 버전 관리 방식의 예제를 포함해야 한다.
문제 8: JWT 인증을 활용한 API 보안 적용
JWT(Json Web Token)를 사용하여 API 요청을 보호하는 기능을 추가하려고 한다. 아래 요구사항을 만족하는 JWT 인증 필터 클래스를 설계하시오.

클라이언트가 Authorization: Bearer <token> 형식의 헤더를 포함하여 요청하면 인증을 수행한다.
유효한 토큰이 없는 경우 401 Unauthorized 상태 코드를 반환해야 한다.
인증이 성공하면 요청을 계속 진행할 수 있도록 한다.
요구사항:

Spring Security 또는 필터 기반 인증을 고려하여 설계해야 한다.
유효하지 않은 토큰일 경우 적절한 오류 응답을 반환해야 한다.
문제 9: RESTful API 응답 캐싱 적용
API 응답 속도를 개선하기 위해 @Cacheable을 활용하여 특정 엔드포인트의 응답을 캐싱하는 코드를 설계하시오.

GET /products 요청 결과를 캐싱하도록 설정한다.
캐싱 만료 시간을 10분으로 설정한다.
캐시 키는 메서드 이름을 기준으로 설정한다.
요구사항:

Spring Boot의 캐싱 기능을 활용해야 한다.
적절한 캐시 관리 전략을 반영해야 한다.
문제 10: Swagger(OpenAPI) 문서화 적용
Spring Boot에서 Swagger(OpenAPI)를 설정하여 API 문서화를 구성하는 방법을 설명하시오.

/api-docs 경로에서 API 문서를 제공하도록 설정한다.
API 그룹을 v1, v2로 나누어 문서화한다.
API 문서에 기본적인 정보(제목, 버전, 설명)를 포함한다.
요구사항:

OpenAPI 3.0 표준을 기반으로 API 문서를 작성해야 한다.
API 버전별로 문서를 관리하는 방안을 포함해야 한다.
답안
1. RESTful API의 고급 설계 원칙
1.1. RESTful API 설계 개요
1.1.1 질문에 대한 답안
RESTful API가 클라이언트-서버 구조를 따르는 이유는 무엇인가?

클라이언트와 서버의 역할을 분리하면 개발 및 유지보수가 용이해진다. 서버는 데이터를 제공하는 역할을 하며, 클라이언트는 데이터를 활용하는 역할을 담당한다. 이를 통해 확장성과 보안성이 향상된다.
RESTful API에서 무상태(stateless) 원칙이 중요한 이유는 무엇인가?

무상태 원칙을 따르면 서버가 클라이언트의 이전 요청을 기억할 필요가 없다. 이로 인해 서버의 확장성이 향상되며, 각 요청이 독립적으로 처리될 수 있어 로드 밸런싱이 원활하게 이루어진다.
1.2. 리소스 설계 원칙
1.2.1 질문에 대한 답안
RESTful API에서 엔드포인트 URL을 동사(Verb) 기반이 아닌 명사(Noun) 기반으로 설계하는 것이 중요한 이유는 무엇인가?

RESTful API는 리소스를 중심으로 설계되므로, 엔드포인트는 리소스를 명확하게 표현해야 한다. 동사가 포함되면 URL이 불필요하게 길어지고, HTTP 메서드와 역할이 중복될 수 있다.
리소스 간 계층적 구조를 적용하면 어떤 이점이 있는가?

계층적 구조를 적용하면 API의 직관성이 향상되며, 특정 리소스에 속하는 하위 리소스를 쉽게 구별할 수 있다. 예를 들어, /users/{userId}/orders/{orderId}와 같은 구조를 사용하면 특정 사용자의 주문을 명확하게 식별할 수 있다.
1.2.2 실습 문제에 대한 답안
문제 1: RESTful URL 설계하기

/products
/products/{id}
POST /products
DELETE /products/{id}
문제 2: HTTP 메서드와 엔드포인트 매핑

GET /customers
POST /customers
PUT /customers/{id}
DELETE /customers/{id}
1.3. 상태 전이와 API 설계
1.3.1 질문에 대한 답안
RESTful API에서 상태 전이(State Transition)의 개념이 중요한 이유는 무엇인가?

클라이언트가 서버와 상호작용하면서 리소스의 상태를 변경해야 하는 경우가 많다. RESTful API는 이를 HTTP 메서드를 통해 해결하며, 상태 전이를 적절히 설계하면 API의 일관성이 유지된다.
PUT과 PATCH 메서드는 어떻게 다르고, 각각 어떤 상황에서 사용하는 것이 적절한가?

PUT은 리소스를 전체적으로 갱신할 때 사용하며, 제공되지 않은 필드는 기본값으로 덮어씌워진다. 반면 PATCH는 특정 필드만 수정할 때 사용하여 불필요한 데이터 변경을 방지한다.
2. RESTful API에서 HTTP 상태 코드 활용
2.1. HTTP 상태 코드 개요
2.1.1 질문에 대한 답안
HTTP 상태 코드는 왜 필요한가?

HTTP 상태 코드는 클라이언트가 서버의 응답을 올바르게 해석할 수 있도록 돕는다. 이를 통해 요청의 성공 여부, 클라이언트의 오류, 서버의 문제 등을 명확하게 전달할 수 있다.
2xx, 4xx, 5xx 상태 코드의 주요 차이점은 무엇인가?

2xx는 성공적인 요청을 나타내고, 4xx는 클라이언트의 오류(잘못된 요청 등)를 의미하며, 5xx는 서버 내부 오류를 나타낸다.
2.2. 상태 코드별 활용 사례
2.2.1 질문에 대한 답안
HTTP 상태 코드 201 Created와 204 No Content의 차이점은 무엇인가?

201 Created는 새로운 리소스가 생성되었을 때 사용되며, 응답 본문에 생성된 리소스의 정보가 포함될 수 있다. 204 No Content는 요청이 성공적으로 처리되었지만 응답 본문이 필요하지 않을 때 사용된다.
클라이언트가 서버에 존재하지 않는 리소스를 요청했을 때 적절한 상태 코드는 무엇이며, 왜 404 Not Found를 사용하는가?

404 Not Found는 요청한 리소스가 존재하지 않음을 나타낸다. 이는 클라이언트가 잘못된 URL을 요청했거나 삭제된 리소스를 요청한 경우 적절한 응답이다.
2.2.2 실습 문제에 대한 답안
문제 1: 적절한 HTTP 상태 코드 선택

1. 200 OK
2. 400 Bad Request
3. 404 Not Found
4. 500 Internal Server Error
문제 2: RESTful API 응답 처리

{
  "status": 201,
  "message": "User created successfully",
  "userId": 12345
}
{
  "status": 404,
  "message": "Resource not found"
}
{
  "status": 401,
  "message": "Unauthorized access"
}
2.3. 오류 응답 표준화
2.3.1 실습 문제에 대한 답안
문제 1: 표준화된 오류 응답 설계

{
  "status": 400,
  "error": "Bad Request",
  "message": "Invalid input data",
  "timestamp": "2025-03-11T12:00:00Z"
}
문제 2: 공통 예외 처리 구현

@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<Map<String, Object>> handleValidationException(MethodArgumentNotValidException ex) {
        Map<String, Object> errorResponse = new HashMap<>();
        errorResponse.put("status", 400);
        errorResponse.put("error", "Bad Request");
        errorResponse.put("message", "Invalid input data");
        errorResponse.put("timestamp", Instant.now());
        return ResponseEntity.badRequest().body(errorResponse);
    }

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<Map<String, Object>> handleResourceNotFoundException(ResourceNotFoundException ex) {
        Map<String, Object> errorResponse = new HashMap<>();
        errorResponse.put("status", 404);
        errorResponse.put("error", "Not Found");
        errorResponse.put("message", ex.getMessage());
        errorResponse.put("timestamp", Instant.now());
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(errorResponse);
    }
}
3. API 버전 관리 전략
3.1. API 버전 관리 필요성
3.1.1 질문에 대한 답안
API 버전 관리는 왜 필요한가?

기존 클라이언트와의 호환성을 유지하면서 새로운 기능을 추가하거나 기존 기능을 개선할 수 있도록 하기 위함이다. 버전 관리가 없으면 API의 변경이 기존 사용자를 방해할 수 있다.
URL을 이용한 버전 관리(/v1/users)와 요청 헤더 기반 버전 관리(Accept: application/vnd.api.v1+json) 방식의 장단점은 무엇인가?

URL 기반 버전 관리는 직관적이지만, API 엔드포인트가 많아질 경우 유지보수가 어려울 수 있다. 반면, 요청 헤더 기반 버전 관리는 API의 URL을 유지할 수 있지만, 클라이언트가 적절한 헤더를 설정해야 하는 부담이 있다.
3.2. API 변경 시 고려 사항
3.2.1 질문에 대한 답안
하위 호환성을 유지하기 위해 API에서 필드 변경 시 고려해야 할 점은 무엇인가?

기존 클라이언트가 정상적으로 동작하도록 변경해야 하며, 필드를 제거하는 대신 새로운 필드를 추가하는 방식으로 변경하는 것이 좋다.
새로운 버전을 제공할 때 기존 버전의 수명을 어떻게 관리해야 하는가?

일정 기간 동안 구버전을 유지한 후 공식적인 Deprecation 공지를 제공하고 점진적으로 제거하는 것이 바람직하다.
4. HATEOAS(Hypermedia as the Engine of Application State)
4.1. HATEOAS 개념과 필요성
4.1.1 질문에 대한 답안
HATEOAS는 RESTful API에서 어떤 역할을 하는가?

HATEOAS는 API 응답에 관련된 리소스에 대한 링크를 포함하여 클라이언트가 동적으로 API를 탐색할 수 있도록 한다. 이를 통해 API 사용이 더욱 직관적이고 유연해진다.
HATEOAS가 클라이언트-서버 간 결합도를 줄이는 이유는 무엇인가?

클라이언트가 사전에 정의된 URL을 알 필요 없이 API 응답에서 제공하는 링크를 따라 탐색할 수 있기 때문에 서버 변경이 클라이언트에 미치는 영향을 최소화할 수 있다.
4.2. REST API에서 Hypermedia 적용 방식
4.2.1 실습 문제에 대한 답안
문제 1: REST API 응답에 HATEOAS 적용하기

{
  "orderId": 123,
  "status": "SHIPPED",
  "links": [
    { "rel": "self", "href": "/orders/123" },
    { "rel": "next", "href": "/orders/124" },
    { "rel": "cancel", "href": "/orders/123/cancel" }
  ]
}
문제 2: 상태에 따라 다른 링크 제공하기

{
  "orderId": 456,
  "status": "PENDING",
  "links": [
    { "rel": "self", "href": "/orders/456" },
    { "rel": "cancel", "href": "/orders/456/cancel" }
  ]
}
5. RESTful API 보안 기초
5.1. API 보안 개요
5.1.1 질문에 대한 답안
API를 보호하지 않으면 발생할 수 있는 주요 보안 위협은 무엇인가?

무단 접근, 데이터 유출, DDoS 공격 등의 위험이 발생할 수 있다. 이러한 위협은 서비스 운영에 심각한 영향을 미칠 수 있다.
API 보안을 강화하기 위해 일반적으로 적용하는 주요 보안 기법은 무엇인가?

인증 및 권한 부여(JWT, OAuth 2.0), 데이터 암호화(SSL/TLS), Rate Limiting(요청 제한) 등이 있다.
5.3. CORS(Cross-Origin Resource Sharing) 정책
5.3.1 실습 문제에 대한 답안
문제 1: CORS 설정하기

@Configuration
public class CorsConfig {
    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/api/**")
                        .allowedOrigins("https://example.com")
                        .allowedMethods("GET", "POST");
            }
        };
    }
}
문제 2: 모든 도메인에서 API 요청을 허용하는 CORS 설정 추가

@CrossOrigin(origins = "*", allowedHeaders = "*", methods = {RequestMethod.GET, RequestMethod.POST, RequestMethod.PUT, RequestMethod.DELETE})
@RestController
@RequestMapping("/api")
public class ExampleController {
    @GetMapping("/data")
    public ResponseEntity<String> getData() {
        return ResponseEntity.ok("CORS enabled");
    }
}
6. RESTful API 성능 최적화 기초
6.1. API 성능 최적화 개요
6.1.1 질문에 대한 답안
API 응답 속도를 저하시킬 수 있는 주요 요인은 무엇인가?

불필요한 데이터 로딩, 중복 요청 처리, 비효율적인 데이터베이스 쿼리, 과도한 API 호출 등이 API 성능을 저하시킬 수 있다.
API 성능을 개선하기 위한 일반적인 전략은 무엇인가?

캐싱, 데이터 압축(Gzip), 페이징 및 정렬, 비효율적인 쿼리 최적화, 로드 밸런싱 적용 등이 있다.
7. RESTful API 문서화
7.1. API 문서화 개요
7.1.1 질문에 대한 답안
API 문서화가 중요한 이유는 무엇인가?

API를 사용하는 개발자가 기능을 빠르게 이해하고, 일관된 방식으로 요청을 보낼 수 있도록 돕는다. 문서화가 없으면 API 사용 방법을 파악하는 데 시간이 오래 걸릴 수 있다.
자동화된 API 문서화와 수동 API 문서화의 차이는 무엇인가?

자동 문서화는 코드 기반으로 자동 생성되므로 유지보수가 용이하지만, 수동 문서화는 커스터마이징이 가능하여 상세한 설명을 추가할 수 있는 장점이 있다.
8. 연습 문제에 대한 답안
8.1 RESTful API 엔드포인트 설계

정답:
다음은 도서 관리 시스템에서 RESTful API 엔드포인트를 설계한 예제이다.

기능	HTTP 메서드	엔드포인트
전체 도서 목록 조회	GET	/books
특정 도서 정보 조회	GET	/books/{bookId}
새로운 도서 추가	POST	/books
특정 도서 정보 수정	PUT	/books/{bookId}
특정 도서 삭제	DELETE	/books/{bookId}
8.2 HTTP 상태 코드 매칭

정답:
아래는 각 시나리오에 적절한 HTTP 상태 코드이다.

시나리오	HTTP 상태 코드
존재하지 않는 bookId로 도서 조회 요청	404 Not Found
새로운 도서가 정상적으로 추가됨	201 Created
필수 데이터 없이 요청이 전달됨	400 Bad Request
서버 내부에서 처리 중 예기치 않은 오류 발생	500 Internal Server Error
인증되지 않은 사용자가 도서를 삭제 요청	401 Unauthorized
8.3 표준화된 오류 응답 설계

정답:
다음은 403 Forbidden 상태 코드의 표준화된 오류 응답 JSON 예제이다.

{
  "status": 403,
  "error": "Forbidden",
  "message": "접근 권한이 없습니다.",
  "code": "ERR_403",
  "timestamp": "2025-03-11T12:00:00Z"
}
8.4 HATEOAS 적용

정답:
HATEOAS 원칙을 적용한 주문 상세 응답 JSON 예제이다.

{
  "orderId": 202501,
  "status": "PROCESSING",
  "links": [
    { "rel": "self", "href": "/orders/202501" },
    { "rel": "next", "href": "/orders/202502" },
    { "rel": "cancel", "href": "/orders/202501/cancel" }
  ]
}
조건:

주문 상태가 "PROCESSING"일 경우 cancel 링크가 포함된다.
8.5 CORS 설정 추가

정답:
Spring Boot에서 특정 도메인(https://client-app.com)에서만 GET, POST 요청을 허용하는 CORS 설정 코드이다.

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class CorsConfig {
    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/**")
                        .allowedOrigins("https://client-app.com")
                        .allowedMethods("GET", "POST");
            }
        };
    }
}
8.6 RESTful API의 상태 변화 처리

정답:
주문의 상태를 "DELIVERED"로 변경하는 API 엔드포인트 설계이다.

기능	HTTP 메서드	엔드포인트	요청 본문 예시
주문 상태 변경	PATCH	/orders/9876/status	{ "status": "DELIVERED" }
8.7 RESTful API 버전 관리

정답:
다음은 URL 기반과 요청 헤더 기반 API 버전 관리 방식의 예제이다.

URL 기반 버전 관리

GET /v1/users
GET /v2/users
요청 헤더 기반 버전 관리

GET /users
Header: Accept: application/vnd.api.v1+json
8.8 JWT 인증을 활용한 API 보안 적용

정답:
JWT 인증을 검증하는 Spring Security 필터 클래스 예제이다.

import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;
import org.springframework.util.StringUtils;

import javax.servlet.FilterChain;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class JwtAuthenticationFilter extends UsernamePasswordAuthenticationFilter {

    private final JwtTokenProvider jwtTokenProvider;

    public JwtAuthenticationFilter(JwtTokenProvider jwtTokenProvider) {
        this.jwtTokenProvider = jwtTokenProvider;
    }

    @Override
    protected void doFilterInternal(HttpServletRequest request,
                                    HttpServletResponse response,
                                    FilterChain chain) throws IOException, ServletException {
        String token = resolveToken(request);
        if (token != null && jwtTokenProvider.validateToken(token)) {
            UserDetails userDetails = jwtTokenProvider.getUserDetails(token);
            SecurityContextHolder.getContext().setAuthentication(
                jwtTokenProvider.getAuthentication(userDetails)
            );
        }
        chain.doFilter(request, response);
    }

    private String resolveToken(HttpServletRequest request) {
        String bearerToken = request.getHeader("Authorization");
        if (StringUtils.hasText(bearerToken) && bearerToken.startsWith("Bearer ")) {
            return bearerToken.substring(7);
        }
        return null;
    }
}
8.9 RESTful API 응답 캐싱 적용

정답:
Spring Boot의 @Cacheable을 활용하여 GET /products 요청 결과를 캐싱하는 코드 예제이다.

import org.springframework.cache.annotation.Cacheable;
import org.springframework.stereotype.Service;
import java.util.List;

@Service
public class ProductService {

    @Cacheable(value = "products", key = "'all'", cacheManager = "cacheManager")
    public List<Product> getAllProducts() {
        // 실제 데이터베이스에서 상품 목록 조회
        return productRepository.findAll();
    }
}
조건:

@Cacheable(value = "products", key = "'all'")을 사용하여 캐싱 적용.
캐시 만료 시간은 10분으로 설정.
8.10 Swagger(OpenAPI) 문서화 적용

정답:
Swagger를 설정하여 /api-docs에서 API 문서를 제공하는 방법이다.

의존성 추가 (pom.xml)

<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.0.0</version>
</dependency>
Swagger 설정

import io.swagger.v3.oas.annotations.OpenAPIDefinition;
import io.swagger.v3.oas.annotations.info.Info;
import org.springframework.context.annotation.Configuration;

@Configuration
@OpenAPIDefinition(info = @Info(title = "My API", version = "v1", description = "API 문서"))
public class SwaggerConfig {
}
Swagger 문서 확인

http://localhost:8080/swagger-ui/index.html
닫기
