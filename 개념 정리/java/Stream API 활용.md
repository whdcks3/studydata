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
