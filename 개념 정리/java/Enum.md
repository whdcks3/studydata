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

## 1-3 Enum의 장점
Enum은 Java프로그램에서 매우 유용하며, 다른 데이터 구조보다 여러 면에서 강력한 장점을 제공한다. Enum의 장점은 코드를 작성하고 유지보수하는 과정에서 더욱 빛을 발한다.

### 코드 가독성 향상

**명확한 값 표현**<br>
Enum은 특정 값들의 집합을 명확하게 표현할 수 있다. 예를 들어, 요일을 나타날 때 int나 String 대신 Enum을 사용하면<br>
코드의 의도를 훨씬 직관적으로 전달할 수 있다.<br>
일반적으로 숫자나 문자열로 표현된 값은 의미를 이해하기 어렵지만, Enum은 해당 값의 의미를 바로 알 수 있도록 한다.

```java
// 숫자 값 사용
public static final int MONDAY = 1;
public static final int TUESDAY = 2;

public void printDay(int day) {
    if (day == MONDAY) {
        System.out.println("월요일");
    }
}

// Enum 사용
public enum Day {
    MONDAY, TUESDAY
}

public void printDay(Day day) {
    if (day == Day.MONDAY) {
        System.out.println("월요일");
    }
}
```
첫 번째 코드에서는 숫자 1과 2가 무엇을 의미하는지 문맥을 통해 추축해야 한다.<br>
두 번째 코드에서는 Day.MONDAY라는 이름을 통해 바로 월요일을 나타낸다는 점을 이해할 수 있다.

**코드의 의도 표현**<br>
Enum은 값뿐만 아니라 코드의 의도도 명확히 나타낸다. 예를 들어, 색상 값이 ```RED```,```GREEN```,```BLUE```로 제한되는 경우<br>
Enum을 사용하면 코드 작성자가 해당 값 외의 입력을 방지하고자 했다는 의도를 전달할 수 있다.
```java
public enum Color {
    RED, GREEN, BLUE
}

public void setColor(Color color) {
    System.out.println("색상: " + color);
}
```
위 코드에서 setColor 메소드는 RED,GREEN,BLUE 중 하나의 값만 받을 수 있다. 이로 인해 잘못된 값을 전달할 가능성이 줄어든다.

----------------------
### 에러 방지
**타입 안전성 보장**<br>
Enum은 값이 정해진 집합으로 제한되기 때문에, 잘못된 값을 사용할 가능성을 원칙적으로 차단한다.<br>
예를 들어, 숫자나 문자열을 사용할 경우, 실수로 잘못된 값을 전달할 위험이 있지만, Enum은 이러한 실수를 방지한다.
```java
// 숫자 값 사용 (타입 안전하지 않음)
public void processDay(int day) {
    if (day == 8) { // 잘못된 값
        System.out.println("에러 발생");
    }
}

// Enum 사용 (타입 안전)
public void processDay(Day day) {
    // Day 값만 허용됨
    System.out.println("오늘은 " + day + "입니다.");
}
```


**허용되지 않는 값 차단**<br>
Enum은 프로그램이 잘못된 입력을 받지 않도록 설계된다.
```java
public enum OrderStatus {
    PENDING, SHIPPED, DELIVERED
}

public void updateOrderStatus(OrderStatus status) {
    switch (status) {
        case PENDING:
            System.out.println("주문이 처리 대기 중입니다.");
            break;
        case SHIPPED:
            System.out.println("주문이 배송 중입니다.");
            break;
        case DELIVERED:
            System.out.println("주문이 배송 완료되었습니다.");
            break;
    }
}
```

--------------------
### 유지보수성 강화
**집중된 수정**<br>
Enum은 값의 집합을 한곳에서 관리하므로, 값이 변경되거나 추가될 때 다른 모든 코드를 수정할 필요가 없다.<br>
예를 들어, 새로운 Enum 값을 추가하거나 기존 값을 수정할 경우, Enum 정의만 업데이트하면 된다.
```java
public enum Priority {
    LOW, MEDIUM, HIGH
}

public void printPriority(Priority priority) {
    System.out.println("우선순위: " + priority);
}
```

**읽기 쉬운 코드 작성**<br>
Enum을 사용하면 코드가 단순해지고 명확해져서 유지보수 작업이 수월해진다. 특히 팀 작업에서 다른 개발자가 코드를 이해하고 수정하기가 쉬워진다.

**잘못된 입력에 대한 컴파일러 경고**<br>
Enum은 잘못된 값 사용 시 컴파일 단계에서 오류를 발생시키므로, 런타임에 발생할 수 있는 문제를 줄여준다.

--------------------------
## 2. Enum의 고급 기능
### 2-1 Enum에 메소드 추가
Enum은 단순히 상수 값을 정의하는 것에 그치지 않고, 내부에 메소드를 추가하여 다양한 동작을 구현할 수 있다.<br>
이 기능은 Enum을 데이터와 로직이 결합된 강력한 객체로 변환시키며, 각 상수에 고유한 동작을 부여하거나, 공통적인 로직을 정의하는 데 유용하다.

### Enum 내부에 메소드 정의

