# Optional의 개념
## Optional이란.
```Optional```은 Java 8 에서 도입된 클래스 중 하나로, **값의 존재 여부를 명시적으로 표현**할 수 있는 일종의 컨테이너이다.
간단히 말해, 값이 있을 수도 있고 없을 수도 있는 상황을 안전하게 다루도록 도와준다. null 값을 직접적으로 다루는 대신, ```Optional```을 사용하면 null로 인해 발생할 수 있는 여러 문제를 예방할 수 있다.

Java에서 null은 값이 없음을 나타내기 위해 널리 사용되어 왔다. 하지만 null은 명시적이지 않은 방식으로 값의 부재를 표현하므로, 이를 잘못처리 했을 경우 치명적인 ```NullPointerException```을 발생시킨다. 특히 대규모 프로젝트나 협업 환경에서는 null 참조로 인한 오류가 흔히 발생한다.

```Optional```은 이러한 문제를 해결하기 위해 설계된 클래스로, 다음과 같은 기능을 제공한다.
+ 값이 존재하거나 존재하지 않는 상태를 명확히 표현
+ 값의 유무에 따라 안전하게 동작을 수행할 수 있는 API 제공
+ null 체크의 필요성을 제거하고, 코드의 가독성을 향상

-----------------
## Optional이 해결하려는 문제
```Optional```이 등장하기 전에는 null 값을 처리하기 위해 개발자가 직접 조건문을 작성해야 했다.<br>
하지만 null 처리가 누락되거나 잘못 구현될 경우, 예기지 않은 오류로 이어질 가능성이 높다.

다음은 null로 인해 발생할 수 있는 문제를 보여주는 간단한 예제이다.
```java
public String getUserName(User user) {
    // user가 null이라면 NullPointerException 발생
    return user.getName();
}
```
위 코드는 단순해 보이지만, ```user```객체가 null일 경우 ```getName()```메서드를 호출하는 시점에서 ```NullPointException```이 발생한다. 이 문제를 방지하기 위해 null 체크를 추가하면 코드는 다음과 같이 복잡해진다.

```java
public String getUserName(User user) {
    if (user == null) {
        return "Unknown";
    }
    return user.getName();
}
```
null 체크는 기본적인 방어 기법이지만, 이러한 패턴이 반복될 경우 코드가 지저분해지고 실수를 유발할 가능성이 높아진다.<br>
특히, 메서드 체이닝이나 중첩된 조건문이 있을떄 null 체크는 더욱 복잡해진다.
```Optional```을 사용하면 이 과정을 간소화하고 안정적으로 구현할 수 있다.

------------------
## Optional의 설계 목표
**NullPontException 방지**<br>
null 참조를 직접 다루지 않고, ```Optional```객체를 통해 안전하게 처리한다. null 체크의 누락을 방지하고, 코드의 안정성을 높인다.

**명시적 표현**<br>
값의 부재(null)를 ```Optional```객체로 명시적으로 표현하여, 코드의 의도를 더 잘 드러낼 수 있다.

**코드 가독성 향상**<br>
불필요한 null 체크를 제거하고, 값을 안전하게 처리하는 API를 제공하여 더 간결한 코드를 작성할 수 있다.

-------------
## Optional의 핵심 개념
```Optional```은 본질적으로 값이 있을 수도 없을 수도 있는 상황을 표현하는 컨테이너이다. ```Optional```객체는 다음 두 가지 상태 중 하나를 가질 수 있다.

**값이 존재하는 상태** : Optional객체 내부에 유효한 값이 포함되어 있다.<br>
**값이 없는 상태** : Optional 객체는 비어 있으며, null과 유사한 상태를 나타낸다.

```Optional```의 기본 동작은 null 값을 직접 다루는 대신, 메서드를 통해 값을 안전하게 확인하거나 조작할 수 있도록 한다.

--------------
## Optional의 주요 특징

**값의 유무를 명시적으로 표현**<br>
값이 있을 수도, 없을 수도 있는 상황을 안전하게 관리한다.<br>
값이 없을 경우에도 null이 아니라 "비어 있는" ```Optional```객체를 사용한다.

**메서드 체이닝 지원**<br>
null 체크를 제거하고, 여러 메서드를 안전하게 연속 호출할 수 있다.

**명확한 API 제공**<br>
값의 유무에 따라 적절한 처리를 수행하는 다양한 메서드를 제공한다.

----------
## Optional의 필요성

**NullPointerException 방지**<br>
Java에서 null 참조는 런타임 오류의 주요 원인 중 하나이다. null 처리를 올바르게 구현하지 않으면 ```NullPonterException```이 발생하기 쉽다. ```Optional```은 값의 부재를 명시적으로 표현함으로써 이러한 문제를 해결한다.

null 처리를 포함한 기존 코드
```java
public String getDefaultName(User user) {
    if (user != null && user.getName() != null) {
        return user.getName();
    }
    return "Unknown";
}
```

Optional을 사용한 코드
```java
public String getDefaultName(User user) {
    return Optional.ofNullable(user)
            .map(User::getName)
            .orElse("Unknown");
}
```
위 코드는 Optioanl을 사용했을 때 null 체크가 제거되고, 코드가 더 간결하고 직관적으로 변하는 것을 보여준다.

**메서드 설계의 명확성**<br>
메서드의 반환값이 null일 수 있는 경우, 이를 ```Optional```로 명시적으로 표현하면 호출자가 값을 안전하게 처리할 수 있다.
```java
public Optional<User> findUserById(int id) {
    return Optional.ofNullable(database.findUser(id));
}
```
호출자는 ```Optional```을 통해 값이 없을 가능성을 사전에 인지하고, 이에 맞는 처리를 수행할 수 있다.

**코드의 일관성 유지**<br>
null 값을 직접 다루는 대신, ```Optional```을 사용하는 일관된 방식으로 null 처리를 구현할 수 있다. 이는 코드의 가독성과 유지보수성을 크게 향상시킨다.

--------------------
## Optional 객체 생성 방식
Java 8에서 제공하는 ```Optional``` 클래스는 값을 포함하거나 비어 있는 개체를 생성할 수 있는 다양한 정적 팩토리 메서드를 제공한다. 이러한 메서드들은 각각의 사용 목적에 맞게 설계되었으며, 상황에 따라 적절한 생성 방식을 선택할 수 있다.

+ ```Optional.of(value)```<br>
null이 아닌 값을 포함하는 ```Optional``` 객체를 생성한다.<br>
이 메서드는 값이 반드시 존재한다고 가정할 때 사용하며, 값이 null인 경우에는 ```NullPointerException```이 발생한다.
```java
public Optional<String> createNonNullOptional() {
    String name = "John Doe";
    return Optional.of(name); // name이 null이 아니므로 Optional 객체 생성 성공
}
```
주의사항 : Optional.of(value)는 값이 null일 가능성이 전혀 없는 경우에만 사용해야 한다. 값이 null인 상황에서 호출하면 런타임에 NullPonterException이 발생한다.

+ ```Optional.ofNullable(value)```<br>
값이 null일 수도 있는 상황에서 Optional 객체를 생성한다.<br>
값이 null인 경우, 비어 있는 Optional 객체를 반환한다.<br>
값이 null이 아니면 해당 값을 포함하는 Optional 객체를 생성한다.
```java
public Optional<String> createNullableOptional(String input) {
    return Optional.ofNullable(input); // input이 null이면 비어 있는 Optional 반환
}
```
입력 값이 null일 수도 있는 상황에서 Optional 객체를 생성할 때 적합하다.<br>
예를 들어, 데이터베이스 조회나 외부 API 호출 결과가 null일 가능성이 있을 때 사용한다.

+ ```Optional.empty()```<br>
비어 있는 Optional 객체를 생성한다.<br>
이는 null의 안전한 대안으로, 값이 없음을 명시적으로 표현하는 데 사용된다.
```java
public Optional<String> createEmptyOptional() {
    return Optional.empty(); // 비어 있는 Optional 객체 반환
}
```
------------------
# Optional의 주요 메서드
## isPresent() 메서드
```isPresent()```는 ```Optional```객체 내부에 값이 존재하는지 여부를 확인하는 메서드이다. 이 메서드는 내부 값이 존재하면 ```true```, 그렇지 않으면 ```false```를 반환한다.

**주요 특징**<br>
값을 직접 꺼내지 않고도 ```Optional```객체 내부에 값이 있는지 확인할 수 있다.<br>
값이 있는 경우 추가 작업을 수행할지 결정하는 조건문에서 유용하다.

```java
public class OptionalIsPresentExample {
    public static void main(String[] args) {
        Optional<String> optionalValue = Optional.of("Hello, Optional!");

        if (optionalValue.isPresent()) {
            System.out.println("값이 존재합니다: " + optionalValue.get());
        } else {
            System.out.println("값이 존재하지 않습니다.");
        }
    }
}
출력
값이 존재합니다: Hello, Optional!
```
---------------------
## isEmpty() 메서드
```isEmpty()```는 ```Optional``` 객체가 비어 있는지 확인하는 메서드이다. Java 11에서 새로 추가되었으며, ```isPresent()```의 반대 동작을 수행한다.

**주요 특징**<br>
값이 없으면 ```true```를 반환한다.<br>
값이 있는지 여부를 확인하는 경우 ```!isPresent()```대신 사용할 수 있다.

```java
public class OptionalIsEmptyExample {
    public static void main(String[] args) {
        Optional<String> emptyOptional = Optional.empty();

        if (emptyOptional.isEmpty()) {
            System.out.println("값이 존재하지 않습니다.");
        } else {
            System.out.println("값이 존재합니다: " + emptyOptional.get());
        }
    }
}
출력
값이 존재하지 않습니다.
```

|메서드|반환값|설명|도입 버전|
|:---|:---|:---|:---|
|isPresent()|true/false|값이 존재하는 경우 true 반환|Java 8|
|isEmpty()|true/false|값이 없는 경우 true 반환|Java 11|

-----------------
## 값 접근 및 기본값 처리

### get() 메서드
```get()``` 메서드는 ```Optional``` 객체 내부에 값이 존재할 경우, 그 값을 반환한다. 이 메서드는 가장 기본적인 값 접근 방법이지만, 값이 없을 경우 ```NoSuchElmentException```예외를 발생시킨다.

**특징**<br>
내부 값에 직접 접근할 수 있는 메서드이다.<br>
값이 존재하지 않을 때는 예외가 발생하므로 반드시 값이 있는지 확인한 후 호출해야 한다.

```java
public class OptionalGetExample {
    public static void main(String[] args) {
        Optional<String> optionalValue = Optional.of("Hello, Optional!");

        // 값이 존재하는 경우
        if (optionalValue.isPresent()) {
            String value = optionalValue.get();
            System.out.println("Optional 값: " + value);
        }

        // 값이 없는 경우 예외 발생
        Optional<String> emptyOptional = Optional.empty();
        try {
            String emptyValue = emptyOptional.get();
        } catch (NoSuchElementException e) {
            System.out.println("예외 발생: 값이 존재하지 않습니다.");
        }
    }
}
출력
Optional 값: Hello, Optional!
예외 발생: 값이 존재하지 않습니다.
```
### orElse() 메서드
```orElse()``` 메서드는 ```Optional```객체 내부에 값이 존재하면 해당 값을 반환하고, 값이 없을 경우 기본값을 반환한다.

**특징**<br>
값이 없을 때 대체값을 제공할 수 있다.<br>
항상 기본값을 계산하거나 제공하는 비용이 발생한다.

```java
public class OptionalOrElseExample {
    public static void main(String[] args) {
        Optional<String> optionalValue = Optional.ofNullable(null);

        // 값이 없으므로 기본값 반환
        String result = optionalValue.orElse("기본값");
        System.out.println("결과: " + result);

        // 값이 있을 경우 기본값이 아닌 내부 값 반환
        Optional<String> nonEmptyOptional = Optional.of("Hello, Optional!");
        String nonEmptyResult = nonEmptyOptional.orElse("기본값");
        System.out.println("결과: " + nonEmptyResult);
    }
}
출력
결과: 기본값
결과: Hello, Optional!
```

