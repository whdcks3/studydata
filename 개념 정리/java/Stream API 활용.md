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
