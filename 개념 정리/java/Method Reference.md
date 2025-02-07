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
------------
# Method Reference의 네 가지 유형
## 정적 메소드 참조(Static Method Reference)
정적 메소드 참조는 클래스의 정적 메소드를 참조하여 사용한다. 여기서 정적 메소드란 객체를 생성하지 않고 클래스 레벨에서 호출 가능한 메소드를 의미한다.
이러한 메소드 참조는 주로 입력값을 받아 처리한 결과를 반환하는 메소드와 매핑된다.

정적 메소드 참조의 일반적인 형태는 다음과 같다
```java
ClassName::staticMethod
```
이 형태에서 ClassName은 클래스의 이름이고, saticMethod는 참조하려는 정적 메소드의 이름이다. 이 구문은 함수형 인터페이스와 함께 사용되며, 특정 로직을 간결하게 표현할 수 있다.

### 정적 메소드 참조의 특징
**객체를 생성하지 않음**<br>
정적 메소드는 클래스에 속하며, 메소드 참조를 사용할 때도 객체를 생성할 필요가 없다.
이는 정적 메소드 참조가 메모리 측면에서 더 효율적일 수 있음을 의미한다.

**입력값과 반환값 매칭**<br>
함수형 인터페이스의 추상 메소드 시그니처(매개변수와 반환값)가 정적 메소드와 일치해야 한다.

**재사용성 향상**<br>
자주 사용되는 정적 메소드를 참조하여 여러 곳에서 반복적으로 사용할 수 있다. 코드 중복을 줄이고, 가독성을 높인다.

예제 : Function<T, R>와 정적 메소드 참조
```java
import java.util.function.Function;

public class StaticMethodReferenceExample {
    public static void main(String[] args) {
        // 람다 표현식 사용
        Function<String, Integer> lambdaFunction = s -> Integer.parseInt(s);

        // 정적 메소드 참조 사용
        Function<String, Integer> methodReferenceFunction = Integer::parseInt;

        // 결과 확인
        String number = "123";
        System.out.println("Lambda: " + lambdaFunction.apply(number)); // 123
        System.out.println("Method Reference: " + methodReferenceFunction.apply(number)); // 123
    }
}
출력
Lambda: 123
Method Reference: 123
```

예제 : BiFunction<T, U, R>와 정적 메소드 참조
```java
import java.util.function.BiFunction;

public class StaticMethodReferenceExample {
    public static void main(String[] args) {
        // 람다 표현식 사용
        BiFunction<Integer, Integer, Integer> lambdaFunction = (a, b) -> Math.addExact(a, b);

        // 정적 메소드 참조 사용
        BiFunction<Integer, Integer, Integer> methodReferenceFunction = Math::addExact;

        // 결과 확인
        System.out.println("Lambda: " + lambdaFunction.apply(10, 20)); // 30
        System.out.println("Method Reference: " + methodReferenceFunction.apply(10, 20)); // 30
    }
}
출력
Lambda: 30
Method Reference: 30
```
--------------
## 특정 객체의 인스턴스 메소드 참조(Instance Method Reference of a Particular Object)
특정 객체의 인스턴스 메소드 참조는 특정 객체에 속하는 인스턴스 메소드를 참조하여 사용하는 방식이다. 이 방법은 람다 표현식의 ```a -> object.method(a)```구조를 간소화하여 ```object::method```형태로 표현한다.
즉, 참조되는 메소드는 이미 존재하는 특정 객체의 메소드여야 한다.

이 유형의 메소드 참조는 다음과 같은 형태를 가진다.
```object::methodName```
여기서 object는 특정 객체의 이름이고, methodName은 참조하려는 메소드의 이름이다. 이는 함수형 인터페이스의 추상 메소드와 매개변수 및 반환값이 일치해야 한다.

### 특정 객체의 인스턴스 메소드 참조의 특징
**객체가 이미 존재해야 함**<br>
참조하려는 객체는 메소드 참조를 사용할 시점에 이미 생성되어 있어야 한다.

**람다 표현식의 대체**<br>
특정 객체에서 인스턴스 메소드를 호출하는 람다 표현식을 대체하여 더 간결한 표현이 가능하다.

**명확한 객체 참조**<br>
메소드 참조를 통해 어떤 객체의 메소드가 호출되는지 명확히 드러난다. 이는 가독성을 향상시킨다.

예제 : 문자열 변환기
```java
import java.util.function.Function;

public class InstanceMethodReferenceExample {
    public static void main(String[] args) {
        // 특정 객체 생성
        String sample = "HELLO WORLD";

        // 람다 표현식 사용
        Function<String, String> lambdaFunction = str -> sample.toLowerCase();

        // 특정 객체의 메소드 참조 사용
        Function<String, String> methodReferenceFunction = sample::toLowerCase;

        // 결과 확인
        System.out.println("Lambda: " + lambdaFunction.apply("IGNORED")); // hello world
        System.out.println("Method Reference: " + methodReferenceFunction.apply("IGNORED")); // hello world
    }
}
출력
Lambda: hello world
Method Reference: hello world
```

예제 : 숫자 출력기
```java
import java.util.Arrays;
import java.util.List;

public class InstanceMethodReferenceExample {
    public static void main(String[] args) {
        // 특정 객체 생성
        Printer printer = new Printer();

        // 데이터 리스트
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // 람다 표현식 사용
        numbers.forEach(num -> printer.print(num));

        // 특정 객체의 메소드 참조 사용
        numbers.forEach(printer::print);
    }
}

class Printer {
    public void print(int number) {
        System.out.println("Number: " + number);
    }
}
출력
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
```

### 특정 객체의 인스턴스 메소드 참조의 제한점
**객체 생성 필요**<br>
참조하려는 객체는 반드시 메소드 참조 이전에 생성되어 있어야 한다. 그렇지 않으면 참조가 불가능하다.

**매개변수 조건**<br>
함수형 인터페이스의 추상 메소드와 참조되는 메소드의 매개변수 및 반환값 조건이 일치해야 한다.

**유연성 부족**<br>
객체가 고정되므로, 동적으로 객체를 변경해야 하는 상황에서는 적합하지 않다

----------------
## 특정 타입의 임의 객체의 인스턴스 메소드 참조 (Instance Method Reference of an Arbitrary Object of a Particular Type)
특정 타입의 임의 객체의 인스턴스 메소드 참조는 특정 클래스의 임의의 객체에서 호출되는 인스턴스 메소드를 참조하는 방식이다.<br>
이 방식은 람다 표현식의 ```x -> x.method()```형태를 간소화하여 ```ClassName::methodName```형태로 표현한다. 이 유형의 메소드 참조는 주로 스트림이나 컬렉션과 같은 데이터 처리에서 사용된다.

### 특정 타입의 임의 객체의 메소드 참조의 특징
**임의 객체 참조**<br>
참조되는 메소드는 특정 클래스의 임의의 객체에서 호출되며, 객체는 스트림이나 컬렉션에서 제공된다.

**람다 표현식의 대체**<br>
람다 표현식에서 ```x -> x.method()```와 같은 구조를 대체하여 더 간결한 코드를 작성할 수 있다.

**함수형 인터페이스 매핑**<br>
함수형 인터페이스의 추상 메소드와 참조된 메소드의 매개변수와 반환값이 일치해야 한다.

### 문법 구조
```java
ClassName::methodName
```
ClassName은 메소드 참조에서 사용되는 클래스의 이름이다. methodName은 참조할 메소드의 이름이다.

예제 : 문자열 리스트 정렬
```java
import java.util.Arrays;
import java.util.List;

public class ArbitraryObjectMethodReferenceExample {
    public static void main(String[] args) {
        // 문자열 리스트
        List<String> names = Arrays.asList("Charlie", "Alice", "Bob");

        // 람다 표현식으로 정렬
        names.sort((a, b) -> a.compareTo(b));
        System.out.println("Sorted with Lambda: " + names);

        // 특정 타입의 임의 객체 메소드 참조로 정렬
        names.sort(String::compareTo);
        System.out.println("Sorted with Method Reference: " + names);
    }
}
출력
Sorted with Lambda: [Alice, Bob, Charlie]
Sorted with Method Reference: [Alice, Bob, Charlie]
```

예제 : 문자열 변환
```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class ArbitraryObjectMethodReferenceExample {
    public static void main(String[] args) {
        // 문자열 리스트
        List<String> names = Arrays.asList("charlie", "alice", "bob");

        // 람다 표현식으로 변환
        List<String> uppercaseNamesWithLambda = names.stream()
                                                     .map(name -> name.toUpperCase())
                                                     .collect(Collectors.toList());
        System.out.println("Uppercase with Lambda: " + uppercaseNamesWithLambda);

        // 특정 타입의 임의 객체 메소드 참조로 변환
        List<String> uppercaseNamesWithMethodReference = names.stream()
                                                              .map(String::toUpperCase)
                                                              .collect(Collectors.toList());
        System.out.println("Uppercase with Method Reference: " + uppercaseNamesWithMethodReference);
    }
}
출력
Uppercase with Lambda: [CHARLIE, ALICE, BOB]
Uppercase with Method Reference: [CHARLIE, ALICE, BOB]
```
------------------
## 생성자 참조 (Constructor Reference)
생성자 참조(Constructor Reference)는 클래스의 생성자를 참조하여 객체를 생성하는 방식이다. 이는 람다 표현식에서 객체를 생성하는 코드를 더 간결하고 명확하게 대체할 수 있다.<br>
생성자 참조는 ```ClassName::new```형태로 표현되며, 특정 클래스의 생성자를 호출하여 새로운 객체를 생성하는 데 사용된다.

### 생성자 참조의 특징
**람다 표현식의 단순화**<br>
람다 표현식 ```() -> new ClassName()``` 또는 ```(args) -> new ClassName(args)```를 간단히 ```ClassName::new```로 대체한다.

**다양한 생성자 지원**<br>
기본 생성자, 매개변수를 가진 생성자 등 다양한 형태의 생성자를 참조할 수 있다.

**함수형 인터페이스와의 연계**<br>
함수형 인터페이스의 추상 메소드 시그니처(매개변수와 반환값)가 생성자의 시그니처와 일치해야 한다.

### 생성자 참조의 문법
```java
ClassName::new
```
ClassName은 참조하려는 생성자를 가진 클래스의 이름이다. new는 생성자를 참조하는 의미이다.

예제 : 기본 생성자 참조
```java
import java.util.function.Supplier;

class Person {
    private String name;

    // 기본 생성자
    public Person() {
        this.name = "Default Name";
    }

    public String getName() {
        return name;
    }
}

public class ConstructorReferenceExample {
    public static void main(String[] args) {
        // Supplier 함수형 인터페이스와 생성자 참조
        Supplier<Person> personSupplier = Person::new;

        // Person 객체 생성
        Person person = personSupplier.get();
        System.out.println("Name: " + person.getName());
    }
}
출력
Name: Default Name
```

예제 : 매개변수가 있는 생성자 참조
```java
import java.util.function.Function;

class Employee {
    private String name;

    // 매개변수가 있는 생성자
    public Employee(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

public class ConstructorReferenceExample {
    public static void main(String[] args) {
        // Function 함수형 인터페이스와 생성자 참조
        Function<String, Employee> employeeFunction = Employee::new;

        // Employee 객체 생성
        Employee employee = employeeFunction.apply("John Doe");
        System.out.println("Employee Name: " + employee.getName());
    }
}
출력
Employee Name: John Doe
```

### 생성자 참조와 배열 생성
생성자 참조는 배열을 생성하는 데도 사용할 수 있다. 배열 생성자를 참조할 때는 ```Type[]::new```형식을 사용한다.
```java
import java.util.function.IntFunction;

public class ArrayConstructorReferenceExample {
    public static void main(String[] args) {
        // IntFunction 함수형 인터페이스와 배열 생성자 참조
        IntFunction<String[]> arrayFunction = String[]::new;

        // 길이가 5인 배열 생성
        String[] stringArray = arrayFunction.apply(5);

        System.out.println("Array length: " + stringArray.length);
    }
}
출력
Array length: 5
```
