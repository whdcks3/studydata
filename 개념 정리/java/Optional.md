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
### orElseGet(Supplier) 메서드
```orElseGet()```은 ```orElse()```와 유사하지만, 값이 없을 경우에만 기본값을 생성하도록 ```Supplier```를 사용한다. 이 메서드는 기본값 생성이 비용이 많이 드는 경우에 유용하다.

**특징**<br>
기본값 계산은 값이 없을 때만 수행된다.<br>
```Supplier```를 통해 동적으로 기본값을 생성할 수 있다.

```java
public class OptionalOrElseGetExample {
    public static void main(String[] args) {
        Optional<String> optionalValue = Optional.ofNullable(null);

        // 값이 없으므로 Supplier에서 기본값 생성
        String result = optionalValue.orElseGet(() -> "동적으로 생성된 기본값");
        System.out.println("결과: " + result);

        // 값이 있을 경우 Supplier 호출 생략
        Optional<String> nonEmptyOptional = Optional.of("Hello, Optional!");
        String nonEmptyResult = nonEmptyOptional.orElseGet(() -> "동적으로 생성된 기본값");
        System.out.println("결과: " + nonEmptyResult);
    }
}
출력
결과: 동적으로 생성된 기본값
결과: Hello, Optional!
```
|메서드|동작|주요 활용 사례|
|:---|:---|:---|
|get()|값 변환. 값이 없으면 예외 발생|값이 항상 존재한다고 보장되는 경우|
|orElse()|값이 없을 경우 기본값 반환. 항상 기본값 계산 비용 발생|단순한 기본값이 필요한 경우|
|orElseGet()|값이 없을 경우에만 기본값을 동적으로 생성|기본값 계산 비용이 높거나 동적 생성이 필요한 경우|
|orElseThrow()|값이 없을 경우 지정된 예외 발생|값이 없으면 코드 실행을 중단해야 하는 경우|

------------------
## 값 변환과 필터링
### map(Funtion) 메서드
```map()```메서드는 ```Optional```내부에 값이 존재할 경우, 해당 값을 특정 함수(Function)에 매핑하여 새로운 ```Optional```객체를 반환한다. 이를 통해 값이 있을 때만 변환을 수행하며, 값이 없을 경우에는 변환을 생략하고 빈 ```Optional```을 반환한다.

**특징**<br>
내부 값이 존재할 때만 변환 로직이 실행된다.<br>
값을 직접 반환하지 않고, 변환 결과를 새로운 ```Optional``` 객체로 감싼다.<br>
함수형 인터페이스 ```Function```을 인자로 받아 변환 작업을 수행한다.

```java
import java.util.Optional;

public class OptionalMapExample {
    public static void main(String[] args) {
        Optional<String> optionalValue = Optional.of("Hello");

        // 값이 존재하면 길이를 반환하는 변환 작업 수행
        Optional<Integer> length = optionalValue.map(String::length);
        System.out.println("문자열의 길이: " + length.orElse(0));

        // 값이 없는 경우
        Optional<String> emptyOptional = Optional.empty();
        Optional<Integer> emptyLength = emptyOptional.map(String::length);
        System.out.println("빈 Optional의 길이: " + emptyLength.orElse(0));
    }
}
출력
문자열의 길이: 5
빈 Optional의 길이: 0
```
-------------
### flatMap(Funtion) 메서드
```flatMap()```메서드는 ```Optional```내부에 값이 존재할 경우, 해당 값을 특정 함수(Function)에 매핑하여 중첩된 ```Optional```객체를 평탄화(flatten)한다. 이는 함수의 결과로 또 다른 ```Optional``` 객체를 반환할 때 사용된다.

**특징**<br>
```map()```과는 달리, 변환 결과로 생성된 중첩된 ```Optional```을 하나의 ```Optional```로 평탄화한다.<br>
중첩된 ```Optional<Optional<T>>```대신 ```Optional<T>```를 반환하여 더 간결한 코드를 작성할 수 있게 한다.

```java
import java.util.Optional;

public class OptionalFlatMapExample {
    public static void main(String[] args) {
        // Optional을 반환하는 함수
        Optional<String> optionalValue = Optional.of("12345");

        // 문자열을 정수로 변환하는 과정에서 Optional을 반환
        Optional<Integer> result = optionalValue.flatMap(OptionalFlatMapExample::stringToInt);
        System.out.println("변환 결과: " + result.orElse(0));

        // 빈 Optional을 사용한 경우
        Optional<String> emptyOptional = Optional.empty();
        Optional<Integer> emptyResult = emptyOptional.flatMap(OptionalFlatMapExample::stringToInt);
        System.out.println("빈 Optional의 변환 결과: " + emptyResult.orElse(0));
    }

    private static Optional<Integer> stringToInt(String input) {
        try {
            return Optional.of(Integer.parseInt(input));
        } catch (NumberFormatException e) {
            return Optional.empty();
        }
    }
}
출력
변환 결과: 12345
빈 Optional의 변환 결과: 0
```
--------
## filter(Predicate) 메서드
```filter()```메서드는 ```Optional```내부에 값이 존재하고 주어진 조건(Predicate)를 만족할 경우, 해당 값을 포함하는 새로운 ```Optional```을 반환한다. 조건을 만족하지 않으면 빈 ```Optional```을 반환한다.

**특징**<br>
값이 존재하지 않거나 조건을 만족하지 않으면 빈 ```Optional```을 반환한다.<br>
조건을 만족하는지 여부를 확인할 때 사용한다.

```java
import java.util.Optional;

public class OptionalFilterExample {
    public static void main(String[] args) {
        Optional<Integer> optionalValue = Optional.of(42);

        // 조건을 만족하는 경우
        Optional<Integer> filteredValue = optionalValue.filter(val -> val > 40);
        System.out.println("필터링 결과 (조건 만족): " + filteredValue.orElse(-1));

        // 조건을 만족하지 않는 경우
        Optional<Integer> nonMatchingValue = optionalValue.filter(val -> val < 40);
        System.out.println("필터링 결과 (조건 불만족): " + nonMatchingValue.orElse(-1));
    }
}
출력
필터링 결과 (조건 만족): 42
필터링 결과 (조건 불만족): -1
```

### 메서드 비교
|메서드|동작|주요 활용 사례|
|:---|:---|:---|
|map()|값을 변환하여 새로운 ```Optional```반환|값이 있을 때 간단한 변환 작업 수행|
|flatMap()|값을 변환하고 중첩된 ```Optional```을 평탄화|중첩된 ```Optional```처리 및 간결한 코드 작성|
|filter()|값을 조건에 따라 필터링하여 조건을 만족하지 않으면 빈```Optional```반환|특정 조건을 만족하는 경우에만 값을 전달하거나 작업 수행|

-----------------------
## 기존 null 처리 방식과 Optional 비교
### 기존 null 처리 방식
Java에서 ```Optional```이 도입되기 전에는 null값을 처리하기 위해 주로 조건문(if-else)를 사용했다. 이 방식은 간단하면서도 매우 널리 사용되었지만, 개발 과정에서 몇가지 문제점을 초래했다.
```java
public class NullCheckExample {
    public static void main(String[] args) {
        String value = getValue();

        // 기존 null 체크 방식
        if (value != null) {
            System.out.println("값이 존재합니다: " + value);
        } else {
            System.out.println("값이 없습니다.");
        }
    }

    private static String getValue() {
        // null을 반환할 수도 있음
        return null;
    }
}
출력
값이 없습니다.
```
**문제점**<br>
+ NullPonterException 위험
  + null값을 처리하지 않으면 런타임에 ```NullPointerException```이 발생하여 프로그램이 중단될 수 있다.
  + 개발자가 모든 null 상황을 예측하고 처리해야 하므로 코드의 유지보수가 어려워진다.
+ 가독성 저하
  + null 체크 코드가 반복적으로 등장하여 실제 비즈니스 로직이 묻히는 경우가 많다.
  + 조건문이 중첩도리수록 코드가 복잡해진다.
+ 의미 전달 부족
  + 메서드가 반환하는 null 같은 특별한 의미를 내포할 수 있지만, 단순히 null을 반환하면 개발자가 이 의미를 명확히 파악하기 어렵다.

-------------
## Optional을 활용한 null 처리 방식
```Optional```은 null을 직접 사용하지 않고, 값의 유무를 명시적으로 표현할 수 있는 객체다. 이를 통해 null 체크 로직을 간결하게 작성하고 null로 인한 문제를 방지할 수 있다.

```java
import java.util.Optional;

public class OptionalCheckExample {
    public static void main(String[] args) {
        Optional<String> optionalValue = getOptionalValue();

        // Optional을 활용한 null-safe 처리
        optionalValue.ifPresentOrElse(
            value -> System.out.println("값이 존재합니다: " + value),
            () -> System.out.println("값이 없습니다.")
        );
    }

    private static Optional<String> getOptionalValue() {
        // 비어 있는 Optional을 반환하거나 값을 포함할 수 있음
        return Optional.empty();
    }
}
출력
값이 없습니다.
```

**장점**
+ NullPointerException 방지
  + Optional 객체 내부에서 null을 안전하게 처리하므로, 개발자는 null 체크 로직을 직접 작성하지 않아도 된다.
+ 가독성 개선
  + 조건문 대신 ```ifPresent```,```orElse```,```map```등의 메서드를 사용하여 null-safe 코드를 간결하게 작성할 수 있다.
+ 의미 전달
  + 반환값이 있을 수도 없을 수도 있음을 Optional 타입으로 명시적으로 표현한다.
  + 메서드를 사용하는 개발자는 null 가능성을 명확히 이해할 수 있다.

### 기존 null 처리 방식과 Optional의 비교
|항목|기존 null 처리 방식|Optional 사용|
|:----|:----|:----|
|안전성|null을 처리하지 않으면 NullPointerException 발생 가능|Optional 내부에서 null-safe 처리가 자동으로 이루어짐|
|가독성|null 체크 로직이 반복되며 코드가 장황해짐|메서드 체이닝을 사용하여 간결하고 읽기 쉬운 코드 작성|
|의미 전달|null이 반환될 수 있다는 것을 명시적으로 표현하지 못함|Optional 타입으로 값의 유무를 명확히 전달|
|적용 범위|모든 상황에서 사용할 수 있으나, 개발자가 null을 직접 처리해야 함|반환값이 있을 수도 없을 수도 있는 경우에 적합, 필수 값에는 사용하지 않는 것이 권장됨|

---------------------
## 메서드 체이닝의 개념
메서드 체이닝(Method Chaining)은 메서드를 연속적으로 호출하여 한 줄의 코드에서 여러 작업을 처리하는 프로그래밍 방식이다. ```Optional```클래스는 이러한 체이닝 방식을 통해 null-safe한 코드 작성을 지원한다.

메서드 체이닝을 활용하면 각 메서드 호출이 값을 처리하고, 그 결과를 다음 메서드 호출로 전달된다. 이를 통해 null체크와 같은 반복적인 코드 없이도 안전하고 간결하게 값을 변환하거나 필터링할 수 있다.

## Optional을 활용한 메서드 체이닝
```Optional```은 체이닝을 지원하는 여러 메서드를 제공한다. 대표적인 메서드로는 ```map```,```flatMap```,```filter```,```orElse```등이 있다. 각 메서드는 안전하게 값을 처리하거나 조건을 확인한 뒤, 결과를 다음 작업으로 전달한다.

```java
import java.util.Optional;

public class OptionalChainingExample {
    public static void main(String[] args) {
        User user = new User("John", null);

        // 메서드 체이닝을 통한 null-safe 값 처리
        String country = Optional.ofNullable(user)
                .map(User::getAddress)
                .map(Address::getCountry)
                .orElse("Unknown");

        System.out.println("Country: " + country);
    }
}

class User {
    private String name;
    private Address address;

    public User(String name, Address address) {
        this.name = name;
        this.address = address;
    }

    public Address getAddress() {
        return address;
    }
}

class Address {
    private String country;

    public Address(String country) {
        this.country = country;
    }

    public String getCountry() {
        return country;
    }
}
출력
Country: Unknown
```
설명<br>
```Optional.ofNullable(user)``` : User 객체가 null일 수도 있음을 고려하여 Optionalf로 감싼다.<br>
```map(User::getAddress)``` : User 객체에서 Address를 추출하여, null 일경우 Optional.empty()를 반환한다.<br>
```map(Address::getCountry)``` : Address 객체에서 country 값을 추출한다.<br>
```orElse("Unknown")``` : 체이닝 도중 값이 없으면 기본값 "Unknown"을 반환한다.

---------------------
## 체이닝을 활용한 복잡한 로직 처리
```Optional```의 메서드 체이닝은 데이터 변환 및 필터링에도 유용하다.

```java
import java.util.Optional;

public class OptionalFilteringExample {
    public static void main(String[] args) {
        User user = new User("Alice", new Address("USA"));

        // 특정 조건을 기반으로 값 처리
        String country = Optional.ofNullable(user)
                .map(User::getAddress)
                .filter(address -> "USA".equals(address.getCountry()))
                .map(Address::getCountry)
                .orElse("Not from USA");

        System.out.println("Country: " + country);
    }
}
출력
Country: USA
```
--------------
## 실무에서의 활용 사례
### 데이터베이스 조회와 Optional
데이터베이스와 같은 외부 시스템에서 데이터를 조회할 때는 조회 결과가 항상 존재하지 않을 가능성을 고려해야 한다. 예를 들어, 특정 ID에 해당하는 데이터가 없거나 조회 조건이 충족되지 않는 경우가 대표적이다. 이러한 상황에서 null을 반환하는 대신 Optional을 사용하면 결과를 안전하게 처리할 수 있다.

```java
import java.util.Optional;

public class DatabaseExample {
    public static void main(String[] args) {
        UserRepository repository = new UserRepository();

        // 사용자 ID로 조회
        String userName = repository.findUserNameById(1)
                .orElse("Unknown User");

        System.out.println("User Name: " + userName);
    }
}

class UserRepository {
    public Optional<String> findUserNameById(int id) {
        // 데이터베이스 조회 시도 (예제에서는 간단히 null로 처리)
        if (id == 1) {
            return Optional.of("Alice");
        } else {
            return Optional.empty(); // 값이 없음을 명시적으로 표현
        }
    }
}
출력
User Name: Alice
```
---------------
## API 응답 처리와 Optional
API 응답 데이터를 처리할 때도 Optional은 null-safe 코드를 작성하는 데 유용하다, 예를 들어 클라이언트로부터 특정 데이터를 요청받았을 때, 해당 데이터가 없더라도 코드가 에외를 발생시키지 않고 기본값을 반환하거나 적절한 처리를 할 수 있도록 한다.

```java
import java.util.Optional;

public class ApiResponseExample {
    public static void main(String[] args) {
        ApiService apiService = new ApiService();

        // API 응답 데이터 처리
        String result = apiService.getUserEmail(10)
                .map(email -> "Email found: " + email)
                .orElse("Email not found");

        System.out.println(result);
    }
}

class ApiService {
    public Optional<String> getUserEmail(int userId) {
        // 예제에서는 임의로 데이터가 없음을 시뮬레이션
        if (userId == 1) {
            return Optional.of("alice@example.com");
        } else {
            return Optional.empty(); // 데이터가 없음을 명시적으로 반환
        }
    }
}
출력
Email not found
```
