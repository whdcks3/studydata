# Method Reference의 기본 개념
## 메소드 참조란.
메소드 참조(Method Reference)는 Java 8에서 도입된 기능으로, **이미 정의된 메소드를 참조하여 람다 표현식을 간단하게 대체**하는 방식이다<br>
함수형 프로그래밍에서는 메소드나 함수를 다른 함수의 인자로 전달하거나, 데이터 처리를 위한 연산으로 사용할 때가 많다. Java에서도 람다 표현식이 도입되면서 이러한 작업이 가능해졌지만, 여전히 간단한 연산조차 장황하게 느껴지는 경우가 있었다.

```java
list.forEach(item -> System.out.println(item));
```
item -> System.out.println(item) 이라는 람다 표현식은 본질적으로 System.out.println이라는 메소드를 호출하는 역할만 한다. 이처럼 단순히 메소드를 호출하기 위한 람다 표현식은 메소드 참조를 사용하여 더욱 간결하게 작성할 수 있다.<br>
메소드 참조를 사용하면 다음과 같이 바뀐다.
```java
list.forEach(System.out::println);
```
이 코드는 위의 람다 표현식과 완전히 동일한 동작을 하지만, 더 짧고 명확하다. 특히 System.out::println이라는 구문은 해당 메소드가 호출될 것임을 직관적으로 알 수 있게 한다.

-----------
## 메소드 참조가 제공하는 주요 이점
**코드의 간결성**<br>
람다 표현식에서 불필요한 부분을 제거하여 더욱 짧고 간결한 코드를 작성할 수 있다.<br>
특히, 메소드 이름을 그대로 사용함으로써 코드의 목적이 명확히 드러난다.

**가독성 향상**<br>
메소드 참조는 메소드 이름 자체로 동작을 설명하므로, 다른 개발자들이 코드를 더 쉽게 이해할 수 있다.

**재사용성**<br>
람다 표현식 대신 기존의 메소드를 참조함으로써 중복을 줄이고, 도일한 로직을 여러 곳에서 활용할 수 있다.

-----------------
## 메소드 참조의 기본 문법
**정적 메소드 참조** : ```ClassName::methodName```<br>
클래스의 정적 메소드를 참조할 때 사용한다.<br>
예 : ```Math::abs```

**특정 객체의 인스턴스 메소드 참조** : ```instance::methodName```<br>
특정 객체의 인스턴스 메소드를 참조할 때 사용한다.<br>
예 : ```System.out::println```

**임의 객체의 인스턴스 메소드 참조** : ```ClassName::methodName```<br>
특정 클래스의 임의 객체의 메소드를 참조할 때 사용한다.<br>
예 : ```String::toUpperCase```

**생성자 참조** : ```ClassName::new```<br>
생성자를 참조하여 객체를 생성할 때 사용한다.<br>
예 : ```ArrayList::new```

---------------
## 메소드 참조의 동작 원리
메소드 참조는 Java 컴파일러가 람다 표현식의 매개변수와 반환값이 일치하는 메소드를 자동으로 찾아 이를 호출하도록 처리한다<br>
따라서, 메소드 참조를 사용하려면 다음 조건을 만족해야 한다.

**함수형 인터페이스와의 호환성**<br>
메소드 참조가 함수형 인터페이스의 메소드 시그니처와 일치해야 한다. 예를 들어, ```Consumer<T>```의 ```accept(T t)``` 메소드는
매겨변수가 하나이고 반환값이 없으므로, ```System.out::println```과 같은 메소드와 일치해야 한다.

**정의된 메소드의 매겨변수와 반환값이 일치**<br>
참조되는 메소드의 매개변수와 반환값이 함수형 인터페이스의 추상 메소드와 일치해야 한다.

------------------
**메소드 참조의 예제 : 기본 활용**
아래는 정적 메소드를 참조하여 리스트의 각 요소를 처리하는 예제이다.
```java
import java.util.Arrays;
import java.util.List;

public class StaticMethodReference {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, -2, 3, -4, 5);

        // 기존 람다 표현식
        numbers.stream()
               .map(n -> Math.abs(n))
               .forEach(n -> System.out.println(n));

        // 메소드 참조
        numbers.stream()
               .map(Math::abs)
               .forEach(System.out::println);
    }
}
```

**특정 개체의 인스턴스 메소드 참조**<br>
특정 객체의 메소드를 참조하여 데이터를 처리하는 예제이다.
```java
import java.util.function.Consumer;

public class InstanceMethodReference {
    public static void main(String[] args) {
        String message = "Hello, Method Reference!";

        // 특정 객체의 메소드 참조
        Consumer<String> printer = System.out::println;
        printer.accept(message); // 출력: Hello, Method Reference!
    }
}
```

**임의 객체의 인스턴스 메소드 참조**<br>
특정 타입의 임의 객체에서 메소드를 호출하는 예제이다.
```java
import java.util.Arrays;
import java.util.List;

public class ArbitraryObjectMethodReference {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("alice", "bob", "charlie");

        // 기존 람다 표현식
        names.stream()
             .map(name -> name.toUpperCase())
             .forEach(name -> System.out.println(name));

        // 메소드 참조
        names.stream()
             .map(String::toUpperCase)
             .forEach(System.out::println);
    }
}
```
------------------
# Method Reference의 구조
## 메소드 참조의 일반적인 구조
메소드 참조는 클래스나 객체의 기존 메소드를 재사용하기 위한 Java 8 에서 도입된 문법이다. 메소드 참조는 람다 표현식과 달리 매개변수의 전달이나 메소드 호출의 구체적인 구조를 신경 쓰지 않아도 된다.
즉, 개발자가 메소드의 이름만 사용하여 간결하고 읽기 쉬운 코드를 작성할 수 있게 된다.

메소드 참조의 기본 구조는 다음과 같다<br>
+ 클래스명이나 객체명 : 메소드 참조의 주체를 나타낸다.
+ 콜론 두 개(```::```) : 메소드 참조를 지정하기 위해 사용된다.
+ 메소드명 : 호출하려는 메소드의 이름

## 메소드 참조의 문법 형식
**정적 메소드 참조**
```java
ClassName::staticMethod
```

**특정 객체의 인스턴스 메소드 참조**
```java
instance::instanceMethod
```

**임의 객체의 인스턴스 메소드 참조**
```java
ClassName::instanceMethod```
```

**생성자 참조**
```java
ClassName:new
```
----------------
## 메소드 참조의 기초 예제

**정적 메소드  참조 예제**<br>
```Math```클래스의 ```abs```메소드를 메소드 참조로 사용한다.
```java
import java.util.function.Function;

public class StaticMethodReferenceExample {
    public static void main(String[] args) {
        Function<Integer, Integer> absoluteValue = Math::abs;

        // 결과 출력
        System.out.println("Absolute value of -10: " + absoluteValue.apply(-10));
    }
}
출력
Absolute value of -10: 10
```

**특정 객체의 인스턴스 메소드 참조 예제**<br>
특정 객체가 이미 생성되어 있는 경우, 그 객체의 인스턴스 메소드를 참조할 수 있다.
```java
import java.util.function.Consumer;

public class InstanceMethodReferenceExample {
    public static void main(String[] args) {
        String greeting = "Hello, World!";
        Consumer<String> printer = System.out::println;

        // 결과 출력
        printer.accept(greeting); // 메소드 참조로 출력
    }
}
출력
Hello, World!
```

**임의 객체의 인스턴스 메소드 참조 예제**<br>
임의의 객체에 대해 동일한 메소드를 호출하는 경우
```java
import java.util.Arrays;
import java.util.List;

public class ArbitraryObjectMethodReferenceExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // 이름을 대문자로 변환하여 출력
        names.stream()
             .map(String::toUpperCase)
             .forEach(System.out::println);
    }
}
출력
ALICE
BOB
CHARLIE
```

**생성자 참조 예제**<br>
객체 생성을 간결하게 표현하기 위해 생성자 참조를 사용한다.
```java
import java.util.function.Supplier;

public class ConstructorReferenceExample {
    public static void main(String[] args) {
        Supplier<StringBuilder> stringBuilderSupplier = StringBuilder::new;

        // 새 객체 생성
        StringBuilder sb = stringBuilderSupplier.get();
        sb.append("Hello, Constructor Reference!");
        System.out.println(sb.toString());
    }
}
출력
Hello, Constructor Reference!
```
