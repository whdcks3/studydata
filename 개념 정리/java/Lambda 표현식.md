## 람다 표현식이란.
람다 표현식은 Java 8에서 도입된 **익명 함수(Anonymous Function)** 의 한 형태로, 메서드를 간단히 표현할 수 있도록 설계되었다.<br>
전통적으로 Java는 객체지향적 특성을 기반으로 클래스와 메서드의 구조를 엄격히 따랐다. 그러나 람다 표현식은 이러한 제약에서 벗아나 함수형 프로그래밍의 개념을 도입하며 코드의 간결성과 효율성을 높였다.

### 정의
람다 표현식은 메서드를 이름 없이 단일 식(Expressiong)으로 표현하는 방식이다.<br>
이는 Java에서 이름 없는 메서드로 동작하며, 단순한 작업을 짧은 코드로 구현할 수 있다.

### 주요 특징
**함수형 프로그래밍 지원**

Java에 함수형 프로그래밍의 개념을 도입한 핵심 요소이다.<br>
함수형 인터페이스(Functional Interface)와 결합하여 데이터 중심의 처리를 간결하게 구현한다.

**익명성**

람다 표현식은 메서드 이름이 없으며, 익명 함수의 역할을 수행한다.<br>
불필요한 클래스 선언을 제거하여 가독성을 높인다.

**간결성**

코드 중복을 줄이고, 불필요한 구문 없이 작업을 표현할 수 있다.<br>
메서드 정의나 익명 클래스 생성의 번거로움을 해결한다.

**지연 실행 지원**

람다 표현식은 필요할 때만 실행되며, 실행 타이밍을 유연하게 제어할 수 있다.<br>
Stream API 등에서 사용될 때 지연 실행(Lazy Evaluation)의 특성을 활용한다.

-----------------------
## 익명 클래스와 람다 표현식의 비교
람다 표현식은 익명 클래스를 대체하기 위해 설계되었다.<br>
익명 클래스는 간단한 작업에도 불필요하게 많은 코드를 작성해야 하는 단점이 있다.<br>
람다 표현식은 이를 해결하여 가독성과 간결성을 극대화한다.

##### 익명 클래스 예제
```java
Runnable runnable = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello, World!");
    }
};
runnable.run();
```
##### 람다 표현식으로 변환
```java
Runnable runnable = () -> System.out.println("Hello, World!");
runnable.run();
```

#### 차이점 비교
|특징|익명 클래스|람다 표현식|
|:--|:--|:--|
|선언 방식|클래스 선언 및 메서드 구현 필요|함수처럼 간단히 구현 가능|
|코드 길이|장황하고 복잡함|간결하고 짧음|
|가독성|복잡하고 어려움|쉬운 이해 가능|
|사용 목적|복잡한 로직 처리|간단한 작업 처리|
|성능|별도의 클래스 파일 생성 필요|추가 클래스 생성 불필요|

-------------------------------
## 람다 표현식의 기본 구조
람다 표현식은 Java에서 메서드를 간단하게 표현하기 위해 사용되는 문법이며, 매개변수 목록, 화살표 연산자(->), 실행 코드로 구성된다.<br>
이 세 가지 요소가 람다 표현식을 간결하게 만드는 핵심이다.

#### 기본 형식
람다 표현식의 기본형식은 다음과 같다
```java
(매개변수) -> {실행 코드}
```

#### 매개변수 목록
+ 람다표현식에서 입력받는 값들을 정의한다.
+ 매개변수 타입은 생략 가능하며, 컴파일러가 이를 자동으로 추론한다.
+ 매개변수가 하나일 경우 괄호를 생략할 수 있다.
  ```java
    x -> x * x
  ```

#### 화살표 연산자(->)
+ 매개변수와 실행 코드를 구분한다.
+ 매개변수는 화살표 연산자의 왼쪽에, 실행 코드는 오른쪽에 위치한다.

#### 실행 코드
+ 람다 표현식이 수행할 작업을 정의한다.
+ 실행 코드가 한 줄인 경우 중괄호 ```{}```와 ```return```문을 생략할 수 있따.
```java
(a, b) -> a + b
```
실행코드가 여러 줄인 경우 중괄호와 ```return```문을 반드시 작성해야 한다.
```java
(a, b) -> {
    int result = a + b;
    return result;
}
```

#### 예제
두 정수를 더하는 람다 표현식
```java
(int a, int b) -> { return a + b; }
```
타입 생략 및 간소화
```java
(a, b) -> a + b
```
--------------------
### 다양한 표현 방식
람다 표현식은 상황과 필요에 따라 다양한 형태로 표현할 수 있다
Java는 타입 추론과 구문 단순화를 통해 코드를 간결하게 작성하도록 지원한다.

#### 매개변수와 중괄호를 모두 사용하는 방식
가장 명시적인 형태로, 매개변수 타입과, 실행 코드를 모두 작성한다.
```java
(int a, int b) -> { return a + b; }
```

#### 매개변수 타입 생략
컴파일러가 타입을 추론할 수 있으므로 매개변수의 타입을 생략 가능하다.
```java
(a, b) -> { return a + b; }
```

#### 중괄호와 return 생략
실행 코드가 한 줄일 경우, 중괄호와 return 키워드를 생략할 수 있다.
```java
(a,b) -> a + b
```

#### 매개변수가 하나일 경우 괄호 생략
매개변수가 하나라면 괄호()를 생략할 수 있다.
```java
x -> x * x
```

#### 매개변수가 없는 경우
매개변수가 없을 때는 빈 괄호 ()를 사용한다.
```java
() -> System.out.println("Hello, World!")
```
----------------------
### 람다 표현식 사용 시 주의사항
람다 표현식은 간결하지만, 몇 가지 중요한 제약과 사용 규칙이 있다.

#### 매개변수 타입 생략 조건
컴파일러가 매개변수의 타입을 추론할 수 있을 경우에만 생략 가능하다.
```java
(x, y) -> x + y  // 타입 추론 가능
```

#### 중괄호와 return 사용
실행 코드가 여러 줄일 경우에는 중괄호와 return 문을 반드시 사용해야 한다.
```java
(a, b) -> {
    int result = a + b;
    return result;
}
```

#### 타입 추론 실패 사례
컴파일러가 추론할 수 없는 경우 명시적으로 타입을 지정해야 한다.
```java
(Object x, String y) -> x.toString() + y  // 혼합된 타입으로 명시 필요
```

#### 익명 함수의 한계
람다 표현식은 이름이 없는 익명함수로, 상태를 유지하지 못한다. 복잡한 로직이나 상태 관리를 필요로 하는 작업에는 적합하지 않다.

-----------------------
## 람다 표현식과 Funtional Interface
람다 표현식은 자바의 함수형 프로그래밍을 지원하기 위한 핵심 기능이며, Funtional Interface와 밀접한 관계가 있다.<br>
자바에서 람다 표현식은 단독으로 사용할 수 없으며, 반드시 Functional Interface에 의해 참조되어야 한다.<br>
이 파트에서는 Funtional Interface의 개념과 역할, 그리고 람다 표현식과의 연계에 대해 알아보자.

### Functional Interface란.
Funtional Interface는 Java에서 오직 하나의 추상 메서드(abstract method)만을 가지는 인터페이스를 말한다.<br>
Java 8에서 람다 표현식이 도입되면서 함수형 프로그래밍 개념을 지원하기 위해 설계된 구조이다.<br>
함수형 프로그래밍은 데이터를 반환하고 조작하는 작업을 간결하고 직관적으로 표현하는 데 중점을 두며, Funtional Interface는 람다 표현식을 사용하기 위한 기반을 제공한다.

### Funtional Interface의 정의와 역할
#### 단일 추상 메서드(Single Abstract Method, SAM)

Funtional Interface는 단 하나의 추상 메서드를 포함해야 한다.<br>
이 추상 메서드는 람다 표현식을 통해 구현되며, 함수형 프로그래밍의 핵심 원칙인 "함수를 값처럼 전달"하는 개념을 가능하게 한다.

#### 익명 구현체 대체

기존에는 익명 클래스를 사용하여 인터페이스를 구현해야 했다.<br>
Funtional Interface와 람다 표현식을 사용하면 이러한 익명 구현체를 간결하고 효율적으로 대체할 수 있다.

#### Java의 기존 인터페이스와 호환

Java 8 이전에 사용되던 인터페이스 중,단일 추상 메서드를 가진 인터페이스는 모두 Funtional Interface로 간주될 수 있다. 예 : ```Runnable```,```Callable```,```Comparator```

### Functional Interface의 주요 특징
```@FunctionalInterface```어노테이션<br>
Funtional Interface를 명시적으로 표시하기 위해 사용된다.
+ **컴파일 타입 검증**
  이 어노테이션이 적용된 인터페이스가 단일 추상 메서드를 가지지 않으면 컴파일 에러가 발생한다.
+ **선택적 사용**
  어노테이션 없이도 단일 추상 메서드 인터페이스는 Funtional Interface로 동작한다.
+ **권장 사항**
  어노테이션을 추가하면 의도를 명확히 하고, 실수로 다른 추상 메서드를 추가하는 것을 방지할 수 있다.
```java
@FunctionalInterface
interface MyFunctionalInterface {
    void execute(); // 단일 추상 메서드
}
```
추상 메서드 외 메서드 포함 가능하다.

Functional Interface는 **디폴트 메서드(default method)** 와 **정적 메서드(static method)** 를 가질 수 있다.<br>
디폴트 및 정적 메서드는 Funtional Interface의 추상 메서드 규칙에 영향을 미치지 않는다.
```java
@FunctionalInterface
interface AdvancedFunctionalInterface {
    void process(); // 단일 추상 메서드

    default void log(String message) {
        System.out.println("Log: " + message);
    }

    static void display() {
        System.out.println("Static Method in Interface");
    }
}
```
디폴트 메서드 : 인터페이스에 기본 구현을 제공하며, 구현 클래스에서 선택적으로 오버라이드 가능<br>
정적 메서드 : 인터페이스 자체에서 호출 할 수 있는 메서드

### 주요 내장 Funtional Interface
```Predicate<T>```<br>
입력값을 받아 조건을 검증하여 ```boolean```값을 반환<br>
메서드 : ```boolean test(T t)
```java
Predicate<Integer> isEven = x -> x % 2 == 0;
System.out.println(isEven.test(4)); // true
```
```Function<T, R>```<br>
입력값을 변환하여 다른 타입의 결과를 반환<br>
메서드 : ```R apply(T t)
```java
Function<String, Integer> lengthFunction = str -> str.length();
System.out.println(lengthFunction.apply("Hello")); // 5
```
```Consumer<T>```<br>
입력값을 받아 작업을 수행하되, 결과를 반환하지 않음<br>
메서드 : ```void accept(T t)```
```java
Consumer<String> printMessage = msg -> System.out.println(msg);
printMessage.accept("Hello, World!"); // 출력: Hello, World!
```
```Suplier<T>```<br>
입력값 없이 결과를 반환<br>
메서드 :```T get```
```java
Supplier<Double> randomValue = () -> Math.random();
System.out.println(randomValue.get());
```
```BiFunction<T, U, R>```<br>
두 개의 입력값을 받아 하나의 결과를 반환<br>
메서드 : ```R apply(T t, U u)```
```java
BiFunction<Integer, Integer, Integer> multiply = (x, y) -> x * y;
System.out.println(multiply.apply(3, 5)); // 15
```
----------------------
### 람다 표현식과 Functional Interface 사용의 장점
**코드 간결성**

