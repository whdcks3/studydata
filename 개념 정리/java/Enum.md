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
