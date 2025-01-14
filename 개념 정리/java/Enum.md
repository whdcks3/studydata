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
# 2. Enum의 고급 기능
## 2-1 Enum에 메소드 추가
Enum은 단순히 상수 값을 정의하는 것에 그치지 않고, 내부에 메소드를 추가하여 다양한 동작을 구현할 수 있다.<br>
이 기능은 Enum을 데이터와 로직이 결합된 강력한 객체로 변환시키며, 각 상수에 고유한 동작을 부여하거나, 공통적인 로직을 정의하는 데 유용하다.

### Enum 내부에 메소드 정의
Enum 내부에 메소드를 정의하면, Enum 상수와 메소드가 함께 동작하도록 구현할 수 있다. 이는 객체 지향적 설계를 따르는 Java에서 매우 자연스러운 방식이다.
특히, Enum에 메소드를 추가함으로써 각 상수가 독립적인 동작이나 데이터를 가질 수 있다.

**예제 : 메시지를 출력하는 메소드 추가**
```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY;

    // 요일에 따라 메시지를 반환하는 메소드
    public String getMessage() {
        switch (this) {
            case MONDAY:
                return "월요일입니다. 힘내세요!";
            case FRIDAY:
                return "금요일입니다. 주말이 코앞입니다!";
            case SATURDAY:
            case SUNDAY:
                return "주말입니다. 푹 쉬세요!";
            default:
                return "평범한 하루입니다.";
        }
    }
}

public class EnumMethodExample {
    public static void main(String[] args) {
        // 요일에 따른 메시지 출력
        for (Day day : Day.values()) {
            System.out.println(day + ": " + day.getMessage());
        }
    }
}
출력
MONDAY: 월요일입니다. 힘내세요!
TUESDAY: 평범한 하루입니다.
WEDNESDAY: 평범한 하루입니다.
THURSDAY: 평범한 하루입니다.
FRIDAY: 금요일입니다. 주말이 코앞입니다!
SATURDAY: 주말입니다. 푹 쉬세요!
SUNDAY: 주말입니다. 푹 쉬세요!
```
### Enum과 static 메소드
Enum 내부에 static 메소드를 정의하면, Enum과 관련된 유틸리티 기능을 제공할 수 있다. 이는 Enum의 모든 상수에 공통적으로 적용되는 작업을 구현할 때 유용하다.

**예제 :상수 이름으로 Enum 상수 찾기**
```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY;

    // 문자열로 Enum 상수 찾기
    public static Day fromString(String name) {
        for (Day day : Day.values()) {
            if (day.name().equalsIgnoreCase(name)) {
                return day;
            }
        }
        throw new IllegalArgumentException("Invalid day: " + name);
    }
}

public class EnumStaticMethodExample {
    public static void main(String[] args) {
        String input = "friday";

        // 문자열로 Enum 상수 찾기
        Day day = Day.fromString(input);
        System.out.println("입력한 요일: " + day);
    }
}
출력
입력한 요일: FRIDAY
```

### Enum 메소드 활용의 장점
+ 코드의 응집력 증가 : 데이터와 동작이 하나의 Enum에 결합되어, 코드의 응집력이 높아진다.
+ 가독성 향상 : Enum 내부에 메소드를 정의함으로써 코드의 의도가 명확해진다.
+ 유지보수 용이성 : 각 상수에 대해 동작을 추가하거나 수정할 때, Enum 내부에서만 변경하면 된다.
+ 상수별 동작 지원 : Enum 상수별로 서로 다른 동작을 정의하여, 다양한 요구사항을 효과적으로 처리할 수 있다.

----------------
## 3-2 Enum과 생성자
Enum에 생성자를 정의하면 각 Enum 상수에 대해 고유한 속성을 부여하고 이를 초기화할 수 있다. 이는 Enum을 단순한 상수 집합 이상의 객체로 확장하여 더 많은 정보를 저장하고 활용할 수 있게 만든다. 생성자와 속성을 사용하는 Enum은 복잡한 데이터 모델링에도 활용할 수 있어, 코드의 재사용성과 유지보수성을 높인다.

### Enum생성자 정의 방식
**Enum에 생성자 추가**<br>
생성자는 클래스와 마찬가지로 ```private```으로 선언한다. 이는 Enum 상수 외부에서 생성자를 호출할 수 없도록 하기 위한 규칙이다.<br>
생성자는 Enum 상수를 정의하는 부분에서 전달받은 값을 사용하여 초기화된다.

**Enum 상수에 속성 추가**<br> 
Enum 클래스 내부에 인스턴스 변수를 선언하여 속성을 저장한다. 이 변수는 보통 ```final```로 선언하여 변경 불가능하게 만든다.

**Getter 메소드 추가**<br>
Enum 상수에 저장된 속성을 외부에서 읽을 수 있도록 ```getter```메소드를 정의한다.

### 예제 : Enum 생성자와 속성 추가
```java
public enum CoffeeType {
    ESPRESSO(2000), AMERICANO(2500), LATTE(3000), MOCHA(3500);

    private final int price; // 커피의 가격

    // 생성자 정의 (private)
    CoffeeType(int price) {
        this.price = price;
    }

    // Getter 메소드
    public int getPrice() {
        return price;
    }
}

public class CoffeeExample {
    public static void main(String[] args) {
        // 모든 커피의 가격 출력
        for (CoffeeType type : CoffeeType.values()) {
            System.out.println(type + "의 가격: " + type.getPrice() + "원");
        }
    }
}
출력
ESPRESSO의 가격: 2000원
AMERICANO의 가격: 2500원
LATTE의 가격: 3000원
MOCHA의 가격: 3500원
```
### Enum 상수에 복수의 속성 추가
생성자를 활용하면 각 Enum 상수에 복수의 속성을 부여할 수 있다. 이를 통해 Enum 상수가 다양한 정보를 담은 객체로 동작할 수 있게 된다.
```java
public enum CoffeeType {
    ESPRESSO(2000, 5), AMERICANO(2500, 10), LATTE(3000, 120), MOCHA(3500, 150);

    private final int price;    // 커피의 가격
    private final int calories; // 커피의 칼로리

    // 생성자
    CoffeeType(int price, int calories) {
        this.price = price;
        this.calories = calories;
    }

    // Getter 메소드
    public int getPrice() {
        return price;
    }

    public int getCalories() {
        return calories;
    }
}

public class CoffeeDetailExample {
    public static void main(String[] args) {
        // 각 커피의 가격과 칼로리 출력
        for (CoffeeType type : CoffeeType.values()) {
            System.out.println(type + ": 가격=" + type.getPrice() + "원, 칼로리=" + type.getCalories() + "kcal");
        }
    }
}
출력
ESPRESSO: 가격=2000원, 칼로리=5kcal
AMERICANO: 가격=2500원, 칼로리=10kcal
LATTE: 가격=3000원, 칼로리=120kcal
MOCHA: 가격=3500원, 칼로리=150kcal
```

### Enum 생성자와 속성을 사용하는 이유
데이터와 로직의 결합 : Enum 상수와 관련된 데이터를 생성자에서 초기화하여 데이터를 Enum 내부에 결합할 수 있다.
가독성 향상 : Enum 상수별 속성을 코드에 명시적으로 나타내어 가독성을 높인다.
유지보수 용이성 : 데이터와 로직이 하나의 Enum 내부에 있으므로, 수정 시 다른 파일을 탐색할 필요가 줄어든다.
캡슐화 : Enum 내부의 생성자와 속성은 외부에서 직접 수정할 수 없으며, getter 메소드를 통해서만 접근 가능하다.

------------------
# 4. Enum과 Constant 비교
## 4-1 Enum과 상수(Constant)의 차이
```final static```상수와 Enum의 비교
Java에서 Enum과 ```final static``` 상수(Constant)는 모두 변경 불가능한 데이터를 나타내는 데 사용된다. 그러나 두 개념 사이에는 몇 가지 중요한 차이점이 존재한다.

### final static 상수
```final static```키워드를 사용하면 값을 변경할 수 없는 상수를 정의할 수 있다. 보통 클래스나 인터페이스에 선언하며, 상수 값이 바뀌지 않음을 보장한다.
```java
public class ConstantExample {
    public static final int RED = 1;
    public static final int GREEN = 2;
    public static final int BLUE = 3;

    public static void main(String[] args) {
        System.out.println("RED: " + RED);
        System.out.println("GREEN: " + GREEN);
        System.out.println("BLUE: " + BLUE);
    }
}
```

**특징**<br>
간단하고 이해하기 쉬움<br>
숫자나 문자열로만 사용할 수 있음<br>
코드 가독성이 떨어질 수 있음(특히 상수 값이 숫자인 경우)

### Enum
Enum은 상수 집합을 정의할 때 사용하는 더 강력한 방법이다. Enum은 단순히 값을 정의하는 것을 넘어, 추가적인 속성이나 동작(메소드 등)을 함께 정의할 수 있다.
```java
public enum Color {
    RED, GREEN, BLUE
}

public class EnumExample {
    public static void main(String[] args) {
        System.out.println("RED: " + Color.RED);
        System.out.println("GREEN: " + Color.GREEN);
        System.out.println("BLUE: " + Color.BLUE);
    }
}
```
**특징**
상수 값과 관련된 추가 정보를 정의할 수 있음<br>
메소드, 필드 등을 포함하여 객체 지향적으로 설계 가능<br>
코드 가독성과 유지 보수성이 높음

### Enum과 상수의 주요 차이점
**타입 안정성**
+ ```final static```상수는 값 자체를 기반으로 처리하므로 잘못된 값이 전달될 수 있다.
+ Enum은 명확한 타입을 가지므로 컴파일 타임에 잘못된 값을 방지할 수 있다.

```java
public static void printColor(int color) {
    if (color == ConstantExample.RED) {
        System.out.println("Color: RED");
    } else if (color == ConstantExample.GREEN) {
        System.out.println("Color: GREEN");
    } else {
        System.out.println("Invalid Color");
    }
}

// 잘못된 값 전달 가능
printColor(5);  // Output: Invalid Color
```
반면, Enum은 타입 안정성을 제공한다.
```java
public static void printColor(Color color) {
    switch (color) {
        case RED -> System.out.println("Color: RED");
        case GREEN -> System.out.println("Color: GREEN");
        case BLUE -> System.out.println("Color: BLUE");
    }
}

// 잘못된 값 전달 시 컴파일 오류 발생
// printColor(5); // 오류 발생
printColor(Color.RED);  // Output: Color: RED
```

**가독성 및 유지 보수성**
+ ```final static``` 상수는 값이 숫자나 문자열일 경우 코드 가독성이 떨어질 수 있다.
+ Enum은 상수 이름으로 의미를 전달하며, 관련 동작을 함께 정의할 수 있어 유지 보수성이 높다.

**추가 동작 정의**
+ ```final static```상수는 단순한 값만 제공한다.
+ Enum은 각 상수에 메소드나 속성을 추가하여 객체처럼 사용할 수 있다.
```java
public enum Color {
    RED("빨강색"), GREEN("초록색"), BLUE("파랑색");

    private final String description;

    Color(String description) {
        this.description = description;
    }

    public String getDescription() {
        return description;
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println(Color.RED.getDescription()); // Output: 빨강색
    }
}
```
-----------------
## 언제 Enum을 사용하는가?
+ 상수 값이 의미 있는 이름을 가질 때
+ 상수와 관련된 추가 속성이나 동작이 필요할 때
+ 타입 안정성과 코드 가독성을 중요시할 때
