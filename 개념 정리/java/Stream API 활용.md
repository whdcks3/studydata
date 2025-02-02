# Stream API의 기본 동작
Stream API는 데이터를 효율적으로 처리하기 위한 다양한 기능을 제공하며, 데이터의 선택, 변환, 집계, 수집과 같은 작업을 체계적으로 수행할 수 있다.<br>
기본 동작은 크게 중간 연산과 최종연산으로 구분된다.<br>
중간 연산은 데이터를 변환하거나 필터링하는 역할을 하고, 최종 연산은 변환된 데이터를 소비하여 결과를 생성한다.<br>
이 두 가지 동작을 적절히 조합하여 복잡한 데이터 처리 로직을 간결하고 선언적으로 구현할 수 있다.

## 중간 연산
중간 연산은 Stream 데이터의 요소를 변환하거나 필터링하며, 항상 새로운 Stream 객체를 생성하여 반환한다.<br>
이 연산은 **지연 실행(Lazy Evaludation)** 방식을 따르므로, 최종 연산이 호출되기 전까지 실제로 수행되지 않는다.<br>
중간 연산을 활용하면 데이터를 필터링하거나 변환하는 과정을 선언적으로 정의할 수 있으며, 여러 연산은 **체이닝(Pipelining)방식** 으로 연결하여 복잡한 데이터 처리 로직도 간결하게 표현할 수 있다.

--------------
### 1. filter
filter는 지정된 조건에 따라 Stream의 요소를 선택하거나 제외하는 중간 연산이다.<br>
각 요소에 대해 조건(Predicate)를 평가하여, 조건을 만족하는 요소만 새로운 Stream에 포함한다.

**주요 특징**
+ 조건을 만족하는 요소만 필터링하여 Stream에 유지한다.
+ 원본 데이터는 변경되지 않으며, 필터링된 데이터를 새로운 Stream에 저장한다.
+ 불필요한 데이터를 제거하여 효율적인 데이터 처리가 가능하다.

**사용 사례**
+ 정수 리스트에서 짝수만 추출
+ 문자열 리스트에서 특정 키워드를 포함한 문자열만 필터링
+ 데이터베이스 조회 결과에서 조건에 맞는 객체만 선택

#### 메서드 시그니처
```java
Stream<T> filter(Predicate<? super T> predicate)
```
**Predicate**<br>
Stream의 각 요소에 대해 boolean 값을 반환하는 함수형 인터페이스<br>
조건을 true로 평가하면 해당 요소를 유지하고, false로 평가하면 제외한다.

#### 코드 예제
```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class FilterExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
        List<Integer> evenNumbers = numbers.stream()
                                           .filter(n -> n % 2 == 0) // 짝수만 유지
                                           .collect(Collectors.toList());

        System.out.println(evenNumbers); // 출력: [2, 4, 6]
    }
}
```
**실행 흐름**<br>
Stream의 각 요소를 조건(Predicate)로 검사<br>
조건을 만족(true 반환)한 요소만 새로운 Stream에 포함<br>
새로운 Stream 반환

**주의점**<br>
Predicate의 작성 : 조건을 명확히 정의해야 하며, 조건이 복잡할 경우 별도의 메서드로 분리하여 가독성을 유지한다.<br>
지연 실행 : filter 연산 자체는 즉시 실행되지 않으며, 최종 연산이 호출될 때만 평가가 수행된다.

---------------
### 2. map
map은 Stream의 각 요소를 특정 규칙에 따라 변환하거나 가공하여 새로운 Stream을 생성하는 중간 연산이다.<br>
연산 데이터와 다른 형식의 데이터를 생성하거나, 데이터를 변환할 때 사용된다.

**주요 특징**
+ 각 요소에 대해 변환 로직(Function)을 적용한다.
+ 변환된 데이터를 새로운 Stream에 포함하여 반환한다.
+ 데이터를 가공하거나 다른 형식으로 변환하는 데 적합하다.

**사용 사례**
+ 정수 리스트를 문자열 리스트로 변환
+ 객체 리스트에서 특정 필드 값을 추출
+ 입력 데이터를 특정 형식으로 가공하여 새로운 데이터 생성

#### 메서드 시그니처
```java
<R> Stream<R> map(Function<? super T, ? extends R> mapper)
```
**Function**<br>
입력 요소(T)를 받아 변환된 데이터(R)를 반환하는 함수형 인터페이스<br>
변환 로직을 정의하여 각 요소에 적용된다.

#### 코드 예제
```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class MapExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        List<String> upperCaseNames = names.stream()
                                           .map(String::toUpperCase) // 문자열 대문자로 변환
                                           .collect(Collectors.toList());

        System.out.println(upperCaseNames); // 출력: [ALICE, BOB, CHARLIE]
    }
}
```
**실행 흐름**<br>
Stream의 각 요소에 변환 로직(mapper) 적용<br>
변환된 데이터를 포함한 새로운 Stream 생성<br>
변환된 Stream 반환

**주의점**<br>
변환 로직의 복잡성 : 변환 로직이 복잡할 경우, 별도의 메서드 또는 람다 표현식으로 분리하여 코드 가독성을 높인다.<br>
데이터 누락 방지 : map 연산은 입력 데이터의 각 요소에 대해 반드시 하나의 결과를 반환해야 하며, 데이터 누락이 발생하지 않도록 주의한다.

--------------
### 중간 연산의 특징
**지연 실행(Lazy Evaludation)**

중간 연산은 최종 연산이 호출될 때만 실행된다.<br>
불필요한 데이터에 대해 연산이 수행되지 않으므로 성능이 최적화된다.

**체이닝(Pipelining)**

중간 연산은 체이닝 방식으로 연속적으로 연결할 수 있다.<br>
각 연산은 새로운 Stream 객체를 반환하며, 최종 연산 호출 시 모든 중간 연산이 한 번에 실행된다.

**원본 데이터 불변성**

중간 연산은 원본 데이터를 변경하지 않고, 가공된 데이터를 새로운 Stream에 저장한다.<br>
원본 데이터는 그대로 유지되어 안전성이 보장된다.

**다양한 활용 가능성**

중간 연산을 통해 필터링, 변환, 정렬 등의 다양한 데이터 처리 작업을 선언적으로 수행할 수 있다.

---------------
### 중간 연산 사용 시 주의사항

**최종 연산 필수**

중간 연산만 적상하고 최종 연산을 생략하면 Stream은 실행되지 않는다.<br>
데이터를 처리하고 결과를 얻기 위해 반드시 최종 연산을 호출해야 한다.

**효율적인 설계**

중간 연산 체이닝은 간결하지만, 지나치게 복잡한 체이닝은 가독성을 저하시킬 수 있다.<br>
필요한 연산만 포함하여 최적화된 코드를 작성한다.

## 최종 연산
최종 연산은 중간 연산으로 처리된 데이터를 소비하여 결과를 생성하는 역할을 한다.<br>
Stream API에서 최종 연산이 호출되면 Stream은 종료되며, 이후에는 더 이상 사용할 수 없다.<br>
최종 연산은 결과를 단일 값, 컬렉션, 또는 특정 데이터 구조의 형태로 반환한다.

### 1. reduce
reduce는 Stream의 요소를 누적하여 단일 값을 생성하는 최종 연산이다.<br>
초깃값과 누적 로직을 정의하여, Stream의 모든 요소를 축약(Aggregation)한다.

**주요 특징**
+ 데이터를 집계하거나 축약 하는 데 사용한다.
+ 연산 과정에서 초깃값(identity)와 누적 로직(accumulator)를 정의할 수 있다.
+ 연산 결과로 단일 값을 반환하며, 필요에 따라 Optional을 사용할 수 있다.

**사용 사례**
+ 숫자의 합계, 곱셈, 최대값 계산
+ 문자열을 하나의 문장으로 연결
+ 특정 조건에 따라 데이터를 집계

#### 메서드 시그니처
```java
Optional<T> reduce(BinaryOperator<T> accumulator)
T reduce(T identity, BinaryOperator<T> accumulator)
```
**identity**<br>
초깃값으로, 연산의 시작값을 정의한다.<br>
예 : 합계 연산의 초깃값은 0, 곱셈 연산의 초깃값은 1

**accumulator**<br>
두 개의 값을 받아 누적하는 연산 로직을 정의하는 함수형 인터페이스

#### 코드 예제
```java
import java.util.Arrays;
import java.util.List;

public class ReduceExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // 초깃값이 있는 reduce
        int sum = numbers.stream()
                         .reduce(0, Integer::sum); // 합계 계산
        System.out.println("합계: " + sum); // 출력: 합계: 15

        // 초깃값이 없는 reduce
        numbers.stream()
               .reduce(Integer::max) // 최대값 계산
               .ifPresent(max -> System.out.println("최대값: " + max)); // 출력: 최대값: 5
    }
}
```
**실행 흐름**

Stream의 초깃값(identity)를 설정(초깃값이 없는 경우 첫 번째 요소 사용)<br>
Stream의 각 요소를 누적(accumulate)하여 하나의 값으로 축약<br>
최종 결과 반환

**주의점**

초깃값이 없는 reduce는 빈 Stream에서 결과가 없으므로 Optional을 반환한다.<br>
연산 로직(accumulator)이 불명확하거나 복잡하면, 결과의 신뢰성이 낮아질 수 있다.

----------------------
### 2. collect
collect는 Stream의 데이터를 특정 데이터 구조로 수집하는 최종 연산이다.<br>
Stream의 모든 요소를 처리한 결과를 리스트(List),셋(Set),맵(Map) 또는 다른 데이터 구조로 반환한다.

**주요 특징**
+ 결과 데이터를 수집하여 저장하거나 후속 작업에 활용할 수 있다.
+ Collectors 클래스를 통해 다양한 수집 전략을 제공한다.
+ 데이터를 그룹화하거나, 통계값을 계산하는 데도 사용할 수 있다.

**사용 사례**
+ Stream의 요소를 List 또는 Set으로 변환
+ 데이터를 그룹화(Grouping)하거나 분할(Partitioning)
+ 통계값(합계, 평균 등) 계산

**메서드 시그니처**
```java
<R, A> R collect(Collector<? super T, A, R> collector)
```
#### 주요 ```Collectors```메서드
+ toList() : Stream의 요소를 List로 변환
+ toSet() : Stream 요소를 Set으로 변환
+ toMap() : 키-값 쌍으로 데이터를 변환하여 Map으로 변환
+ groupingBy() : 데이터를 특정 기준에 따라 그룹화
+ partitioningBy() : 데이터를 조건에 따라 두 그룹으로 분할

#### 코드 예제
```java
import java.util.*;
import java.util.stream.Collectors;

public class CollectExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "Alice");

        // Set으로 수집 (중복 제거)
        Set<String> uniqueNames = names.stream()
                                       .collect(Collectors.toSet());
        System.out.println("Set: " + uniqueNames); // 출력: Set: [Alice, Bob, Charlie]

        // 리스트를 Map으로 변환
        Map<String, Integer> nameLengthMap = names.stream()
                                                  .distinct() // 중복 제거
                                                  .collect(Collectors.toMap(
                                                      name -> name,        // 키
                                                      name -> name.length() // 값
                                                  ));
        System.out.println("Map: " + nameLengthMap); // 출력: Map: {Alice=5, Bob=3, Charlie=7}
    }
}
```
**실행 흐름**

Stream의 각 요소를 수집 전략(Collector)에 따라 처리<br>
지정된 데이터 구조(List,Set,Map 등)로 결과를 저장<br>
수집된 데이터 반환

**주의점**

Collectors.toMap() 사용 시 키가 중복되면 예외가 발생한다.<br>
중복 키를 허용하거나 병합 전략을 지정하려면 mergeFuction을 추가해야 한다.<br>
데이터 구조의 특성(Set,Map 등)을 고려하여 적절한 Collector를 선택해야 한다.

---------------------------------
### 최종 연산 시 주의사항
**Stream 재사용 불가**<br>
최종 연산이 호출된 Stream은 재사용할 수 없다. 새로운 작업이 필요하다면 Stream을 다시 생성해야 한다.

**Collector 선택** <br>
데이터를 수집할 때 사용되는 Collector를 데이터 처리 목적에 맞게 선택해야 한다.<br>
예 : 중복 제거는 toSet(), 순서 유지 리스트는 toList()

**Optional 처리** <br>
reduce와 같은 일부 연산은 Optional을 반환할 수 있으므로, 결과값이 비어 있을 가능성을 항상 고려해야 한다.

**병렬 처리 유의**<br>
병렬 스트림에서 최종 연산을 사용할 경우, Collector가 병렬 실행에 적합한지 확인해야 한다.<br>
병렬 처리가 올바르게 동작하지 않으면 예외나 잘못된 결과가 발생할 수 있다.

------------------
## Stream의 구조
Stream API는 데이터 처리의 효율성과 간결성을 높이기 위해 데이터 소스, 중간 연산, 최종 연산 으로 구성된 구조를 사용한다.<br>
이 구조는 데이터를 가공하고 변환하여 최종 결과를 생성하는 단계적인 과정을 나타낸다. 이를 통해 데이터 처리 작업을 명확하게 표현할 수 있다.

### Stream의 구성 요소
**데이터 소스(Source)**<br>
Stream은 데이터를 처리하기 위해 반드시 데이터 소스를 필요로 한다.<br>
데이터 소스는 일반적으로 Java의 컬렉션(List, Set, Map 등), 배열, 파일, 혹은 생성 메서드(```Stream.of()```,```Stream.generate()```)에서 생성된다.

**중간 연산(Intermediate Operation)**<br>
중간 연산은 스트림의 데이터를 변환하거나 필터링하는 연산이다. 이러한 연산은 데이터를 바로 처리하지 않고, 새로운 스트림을 반환한다.<br>
중간 연산은 지연 평가(Lazy Evaludation)를 통해 최종 연산이 호출될 때 실제로 실행된다.<br>
예:```filter```,```map```,```sorted```,```distinct```

**최종 연산(Terminal Operation)**<br>
최종 연산은 스트림의 데이터를 소비하고 결과를 반환한다. 이 연산이 호출되면 스트림이 종료되며 더 이상 사용할 수 없게 된다.<br>
예:```forEach```,```collect```,```reduce```

---------------------
## 데이터 처리 흐름
Stream API의 데이터 처리 흐름은 다음과 같은 순서로 이루어진다.
> 데이터 소스 -> 중간 연산 -> 최종 연산
이 구조는 선언적 방식으로 데이터 처리 작업을 작성할 수 있게 하며, 각 단계의 역할을 명확히 구분한다.

### Stream의 구조 간단 에제
```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamExample {
    public static void main(String[] args) {
        // 데이터 소스: List
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David", "Eve");

        // Stream 처리
        List<String> filteredNames = names.stream() // 데이터 소스
                                          .filter(name -> name.startsWith("A")) // 중간 연산
                                          .sorted() // 중간 연산
                                          .collect(Collectors.toList()); // 최종 연산

        // 결과 출력
        System.out.println(filteredNames); // [Alice]
    }
}
```
설명:<br>
데이터 소스 : names라는 List를 스트림으로 변환<br>
중간 연산 : filter:이름이 "A"로 시작하는 요소만 필터링, sorted:알파벳 순서로 정렬<br>
최종 연산 : collect를 사용해 필터링된 데이터를 다시 List로 변환

--------------------
## 데이터 소스
Stream의 데이터 소스는 스트림 생성의 시작점이다. 데이터 소스는 컬렉션, 배열, 파일, 혹은 특정 메서드로부터 생성될 수 있다.

컬렉션(List, Set 등)
Java의 컬렉션 인터페이스는 ```stream()``` 메서드를 통해 스트림을 생성할 수 있다.
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
Stream<Integer> stream = numbers.stream();
```
**배열**<br>
배열은 ```Arrays.stream()```메서드를 통해 스트림을 생성할 수 있다.
```java
int[] numbers = {1, 2, 3, 4, 5};
IntStream stream = Arrays.stream(numbers);
```
**Steam.of()**<br>
정적으로 지정된 요소들로 스트림을 생성할 수 있다.
```java
Stream<String> stream = Stream.of("Alice", "Bob", "Charlie");
```
**무한 스트림**<br>
무한 스트림은 ```Stream.generate()```또는 ```Stream.iterate()```를 사용해 생성된다.
```java
Stream<Integer> infiniteStream = Stream.iterate(0, n -> n + 1);
```
--------------------
## 중간 연산
중간 연산은 데이터 변환과 필터링에 사용된다. 중간 연산은 여러번 체이닝(chain)될 수 있으며, 실제 실행은 최종 연산이 호출될 때까지 지연된다.
```java
Stream<String> stream = Stream.of("Alice", "Bob", "Charlie", "David")
                              .filter(name -> name.length() > 3)
                              .sorted()
                              .map(String::toUpperCase);
```
-----------------
## 최종 연산
최종 연산은 스트림의 데이터를 소비하여 결과를 반환하거나 작업을 수행한다. 최종 연산이 호출되면 스트림은 더 이상 사용할 수 없다.
```java
List<String> result = stream.collect(Collectors.toList()); // 스트림을 리스트로 변환
```
-------------------








-------------------------
### Stream API의 예제

#### 예제1 : 특정 조건으로 데이터 필터링
```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamExample1 {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // 짝수만 필터링
        List<Integer> evenNumbers = numbers.stream()
                                           .filter(n -> n % 2 == 0) // 짝수 조건
                                           .collect(Collectors.toList()); // 결과를 리스트로 수집

        System.out.println("짝수 리스트: " + evenNumbers); // 출력: 짝수 리스트: [2, 4, 6, 8, 10]
    }
}
```
설명<br>
filter 사용 : 각 요소에 조건(짝수)를 검사하여 조건을 만족하는 요소만 유지한다.<br>
Stream 체이닝 : filter로 데이터를 필터링 한 뒤, collect로 리스트에 저장한다.

-----------------------------
#### 예제2 : 데이터 매핑
```java
import java.util.List;
import java.util.stream.Collectors;

public class StreamExample2 {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // 대문자로 변환
        List<String> upperCaseNames = names.stream()
                                           .map(String::toUpperCase) // 대문자로 변환
                                           .collect(Collectors.toList()); // 결과를 리스트로 수집

        System.out.println("대문자로 변환된 이름들: " + upperCaseNames); // 출력: 대문자로 변환된 이름들: [ALICE, BOB, CHARLIE]
    }
}
```
설명<br>
map 사용 : 각 요소에 변환 로직(대문자 변환)을 적용하여 새로운 데이터로 변환한다.<br>
Stream 체이닝 : map으로 데이터를 반환한 뒤, collect로 리스트에 저장한다.

----------------
#### 예제3 : 데이터 누적
```java
import java.util.Arrays;
import java.util.List;

public class StreamExample3 {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // 숫자의 합 계산
        int sum = numbers.stream()
                         .reduce(0, Integer::sum); // 합계 계산

        System.out.println("숫자의 합: " + sum); // 출력: 숫자의 합: 15
    }
}
```
설명<br>
reduce 사용 : 초깃값(0)을 설정하고, 요소를 반복적으로 누적하여 최종 합계를 계산한다.<br>
Stream 체이닝 : Stream의 데이터를 순회하면서 누적 연산을 수행한다.

------------------
#### 예제4 : 데이터 그룹화
```java
import java.util.*;
import java.util.stream.Collectors;

class Student {
    String name;
    int score;

    Student(String name, int score) {
        this.name = name;
        this.score = score;
    }
}

public class StreamExample4 {
    public static void main(String[] args) {
        List<Student> students = Arrays.asList(
            new Student("Alice", 85),
            new Student("Bob", 92),
            new Student("Charlie", 78),
            new Student("David", 88),
            new Student("Eve", 65)
        );

        // 성적 등급별 그룹화
        Map<String, List<Student>> gradeGroups = students.stream()
                                                         .collect(Collectors.groupingBy(
                                                             s -> {
                                                                 if (s.score >= 90) return "A";
                                                                 else if (s.score >= 80) return "B";
                                                                 else if (s.score >= 70) return "C";
                                                                 else return "D";
                                                             }
                                                         ));

        gradeGroups.forEach((grade, group) -> {
            System.out.println("등급: " + grade);
            group.forEach(student -> System.out.println(" - " + student.name + ": " + student.score));
        });
    }
}
```
설명<br>
Collectors.groupingBy 사용 : Stream의 요소를 특정 기준에 따라 그룹화한다.<br>
Stream 체이닝 : 그룹화 기준(등급)을 설정하고 데이터를 그룹별로 수집한다.

---------------------
#### 예제5 : 데이터 분할
```java
import java.util.*;
import java.util.stream.Collectors;

public class StreamExample5 {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // 짝수와 홀수로 분할
        Map<Boolean, List<Integer>> partitioned = numbers.stream()
                                                         .collect(Collectors.partitioningBy(n -> n % 2 == 0));

        System.out.println("짝수: " + partitioned.get(true)); // 출력: 짝수: [2, 4, 6, 8, 10]
        System.out.println("홀수: " + partitioned.get(false)); // 출력: 홀수: [1, 3, 5, 7, 9]
    }
}
```
설명<br>
Collectors.partitioningBy 사용 : Stream의 요소를 조건에 따라 두 그룹으로 분리한다.<br>
Stream 체이닝 : 분할 기준(짝수 여부)를 설정하고 데이터를 그룹별로 분리한다.

--------------------
## 응용과 확장
### 1. 병렬 스트림
병렬 스트림(Parallel Stream)은 데이터를 병렬로 처리하여 성능을 극대화할 수 있는 Stream API의 기능이다.<br>
단일 CPU에서 작업이 직렬로 처리되는 일반 스트림과 달리, 병렬 스트림은 멀티코어 CPU를 활용하여 데이터를 동시에 처리한다.

### 병렬 스트림의 주요 특징
**병렬 처리 방식**<br>
데이터를 여러 청크(chunk)로 나누고, 각각의 청크를 독립적으로 처리한다.<br>
작업 완료 후 결과를 병합(merge)하여 최종 결과를 생성한다.

**자동 병렬화**<br>
Stream API는 병렬 처리의 복잡한 구현을 숨기고, 개발자는 ```parallelSteam()```메서드만 호출하면 병렬 처리가 가능하다.

**스레드 풀 활용**<br>
병렬 스트림은 Java의 ForkJoinPool을 활용하여 내부적으로 작업을 분배하고 병합한다.

-----------------
### 병렬 스트림 생성
병렬 스트림은 두 가지 방법으로 생성할 수 있다.
+ Collection에서 생성
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
numbers.parallelStream()
       .forEach(System.out::println);
```
+ Stream에서 변환
```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5);
stream.parallel()
      .forEach(System.out::println);
```

#### 병렬 스트림 활용 예제
```java
import java.util.stream.IntStream;

public class ParallelStreamExample {
    public static void main(String[] args) {
        long startTime = System.currentTimeMillis();

        // 1부터 1억까지 숫자 중에서 짝수의 합 계산
        int sum = IntStream.rangeClosed(1, 100_000_000)
                           .parallel() // 병렬 스트림으로 변환
                           .filter(n -> n % 2 == 0)
                           .sum();

        long endTime = System.currentTimeMillis();
        System.out.println("합계: " + sum);
        System.out.println("수행 시간: " + (endTime - startTime) + "ms");
    }
}
```

#### 병렬 스트림 사용 시 주의점
**데이터의 순서 보장**<br>
병렬 스트림은 기본적으로 순서를 보장하지 않는다.<br>
순서가 중요한 작업은 ```forEachOrdered```를 사용해야 한다.
```java
numbers.parallelStream()
       .forEachOrdered(System.out::println); // 순서 보장
```
**스레드 안전성**<br>
병렬 스트림에서 공유 자원을 수정하면 데이터 불일치가 발생할 수 있다.<br>
synchronized나 ConcurrentHashMap 등을 활용하여 스레드 안전성을 확보

**작업 복잡도**<br>
병렬 처리의 오버헤드가 작업 시간보다 크다면, 병렬 스트림이 성능을 저하시킬 수 있다.

--------------------

