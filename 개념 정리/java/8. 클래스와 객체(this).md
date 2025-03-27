## 1. 객체지향 프로그래밍(Object-Oriented Programming,OOP).
객체지향 프로그래밍은 현실 세계의 개체(Object)를 코드로 표현하는 프로그래밍 패러다임이다. Java는 객체지향 언어로, 코드를 작성할 때 객체라는 단위로 나누어 작업한다.

##### OOP의 핵심 원칙
+ 캡슐화(Encapsulation) : 데이터와 메소드를 하나의 단위로 묶고, 외부에서 접근을 제한한다.
+ 상속(Inheritance) : 기존 클래스를 확장하여 새로운 클래스를 작성한다.
+ 다형성(Polymorphism) : 동일한 인터페이스나 부모 클래스를 공유하는 객체들이 다양한 방식으로 동작할 수 있게 한다.
+ 추상화(Abstraction) : 중요한 정보만 노출하고 세부적인 구현을 숨기는 기법이다.

----------------------------
## 2. 클래스와 객체란.
Java에서 클래스(Class)는 객체의 속성(데이터)와 행동(기능)을 정의하는 설계도 역할을 한다. **객체(Object)** 는 클래스의 인스턴스로, 클래스에서 정의된 속성과 행동을 실제로 구현하는 데이터 덩어리이다.

---------------------------
## 3. this 키워드의 사용과 생성자 오버로딩
```this```키워드는 클래스의 인스턴스를 가리키며, 주로 메소드나 생성자 내에서 인스턴스 필드와 메소드의 매개변수를 구분하거나, 현재 객체를 참조할 때 사용한다.
생성자 오버로딩은 클래스에 여러 개의 생성자를 정의하여 객체 초기화 시 다양한 방식으로 호출할 수 있게 한다.

##### 예제 : this와 생성자 오버로딩 활용
```java
public class Car {
    private String brand;
    private int speed;

    public Car() {
        this("기본 브랜드", 0); // 다른 생성자 호출
    }

    public Car(String brand) {
        this(brand, 0); // 다른 생성자 호출
    }

    public Car(String brand, int speed) {
        this.brand = brand;
        this.speed = speed;
    }
}

```
