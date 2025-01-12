# Enum의 개념
## 1-1 Enum이란
Enum은 **열거형 데이터 타입**이다. 열거형은 특정한 값들의 고정된 집합을 정의하기 위해 사용된다. 예를 들어, 요일(월요일부터 일요일까지)이나 교통 신호(빨강,노랑,초록)와 같은 데이터처럼 유한한 값들의 범위를 가지는 상황에서 활용된다.
```enum```키워드를 사용하여 정의되며, 각각의 열거형 값은 Java내부에서 **상수 객체**로 간주된다.

**예시**
```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}
```
위 코드에서 Day는 열거형 타입이며, MONDAY부터 SUNDAY까지 7개의 값이 정의되어 있다. 각각의 값은 Day라는 데이터 타입의 인스턴스로 간주된다.
**MONDAY는 문자열이나 숫자가 아니라 Day타입의 값으로 다뤄진다.**

-------
## Enum의 사용 목적
**고정된 값들의 집합 표현**<br>
특정 범위 내에서만 값이 허용되는 경우, Enum을 사용하면 값을 명확히 제한할 수 있다.<br>
예를 들어, 교통 신호는 항상 빨강,노랑,초록 중 하나여야 하며, 이를 문자열이나 정수로 관리한다면 잘못된 값이 포함될 수 있다.<br>
Enum을 사용하면 이러한 잘못된 값을 컴파일 단계에서 차단할 수 있다.
```java
public enum TrafficSignal {
    RED, YELLOW, GREEN
}
```
**거독성과 유지보수성 향상**<br>
Enum은 상수를 문자열이나 숫자로 관리하는 대신 명시적인 이름을 부여해 가독성을 높인다.<br>
예를 들어, ```"RED"```대신 ```TrafficSignal.RED```를 사용하면 코드의 목적과 의미를 명확히 알 수 있다.

**코드 안전성 보장**<br>
Enum을 사용하면 잘못된 값의 입력을 방지할 수 있다. 예를 들어, 문자열 ```"Holiday"```를 입력했을 때 일반 문자열 비교로는 오류를 탐지하기 어렵지만,
Enum 타입을 사용하면 허용된 값 외의 입력을 컴파일 단계에서 걸러낼 수 있다.

### Enum 사용 예제
```java
// Enum 정의
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

// Enum 활용
public class EnumExample {
    public static void main(String[] args) {
        Day today = Day.MONDAY;

        // Enum 값을 출력
        System.out.println("오늘은 " + today + "입니다.");

        // Enum 값을 조건문에서 사용
        if (today == Day.MONDAY) {
            System.out.println("한 주가 시작되었습니다!");
        }
    }
}
출력
오늘은 MONDAY입니다.
한 주가 시작되었습니다!
```

## 1-2 Enum의 특징
### Enum이 일반 클래스와 다른 점
Enum은 Java에서 제공되는 특별한 형태의 클래스다. 그러나 일반적인 클래스와 몇 가지 중요한 차이가 있다. 이 차이점을 이해하면 Enum을 더 효과적으로 사용할 수 있다.

**인스턴스 생성 제한**<br>
Enum은 새로운 객체를 생성할 수 없도록 설계되었다. 즉, ```new```키워드를 사용하여 Enum의 인스턴스를 만들 수 없다.<br>
모든 인스턴스는 Enum 선언 시 정적으로 생성되며, 프로그램 실행 동안 고정된 상태로 유지된다.<br>
이는 **불변성(immutability)** 를 보장하며, 값의 추가, 수정, 삭제를 방지한다.

**예제**
```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY
}

public class Example {
    public static void main(String[] args) {
        // Enum 인스턴스 생성 불가
        // Day newDay = new Day(); // 컴파일 오류 발생

        // Enum 값 접근
        Day today = Day.MONDAY;
        System.out.println(today); // 출력: MONDAY
    }
}
```

**상수로 동작**<br>
Enum의 각 값은 **final static 객체**처럼 동작한다. 이는 Enum 값이 프로그램 실행 중 변경되지 않음을 의미하며, 특정 값들이 고정된 상태로 유지된다. 따라서 값의 무결성을 보정하고, 프로그램 로직의 안정성을 높인다.

**내부적으로 클래스로 처리됨**<br>
Enum은 컴파일러에 의해 내부적으로 java.lang.Enum 클래스를 상속받는 클래스로 변환된다. 따라서 Enum은 ```equals()```,```hasCode()```,```compareTo()```와 같은 메소드를 기본적으로 제공한다.

**자체 메소드 및 필드 추가 기능**<br>
Enum은 단순히 값의 집합으로 사용될 뿐만 아니라, 메소드와 필드를 포함하여 확장할 수 있다. Enum 내부에 메소드를 정의하면 Enum 값을 활용하여 특정 동작을 수행할 수 있다.

**확장된 Enum 예제**
```java
public enum TrafficSignal {
    RED("정지"), YELLOW("준비"), GREEN("출발");

    private final String action;

    // 생성자
    TrafficSignal(String action) {
        this.action = action;
    }

    // 동작 반환 메소드
    public String getAction() {
        return action;
    }
}

public class Example {
    public static void main(String[] args) {
        TrafficSignal signal = TrafficSignal.RED;
        System.out.println(signal.getAction()); // 출력: 정지
    }
}
```

