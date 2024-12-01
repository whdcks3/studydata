# 인스턴스와 static의 차이
자바에서 **인스턴스**와 **static(정적)** 은 객체와 클래스의 메모리 할당 방식과 사용 목적에 따라 중요한 차이가 있다. 이 개념은 프로그램의 메모리 사용과 동작 방식에 큰 영향을 미치며, 적절히 사용하면 **메모리 효율성을 높이고 코드의 재사용성**을 극대화 할 수있다.

## 1. 인스턴스란.
**인스턴스(instance)** 는 클래스의 설계도에 따라 실제 메모리에 생성된 객체를 의미하며, 각 객체는 독립적인 데이터와 메모리 공간을 가지게 된다. 객체를 생성하기 위해서는 ```new```키워드를 사용해야 하며, 인스턴스는 **힙 메모리**에 저장된다.

#### 1-1 인스턴스 필드와 메소드
**인스턴스 필드**는 각 객체가 독립적으로 가지는 데이터로, 각 객체마다 고유한 값을 가질 수 있다.
**인스턴스 메소드**는 인스턴스 필드를 사용하여 작업을 수행하며, 메소드가 호출된 객체의 데이터에 접근하고 조작할 수 있다.
```java
public class Dog {
    String name; // 인스턴스 필드
    int age;     // 인스턴스 필드

    // 인스턴스 메소드: 나이를 증가시키는 메소드
    void birthday() {
        age++;
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog1 = new Dog();  // 첫 번째 Dog 객체 생성
        dog1.name = "Buddy";
        dog1.age = 3;

        Dog dog2 = new Dog();  // 두 번째 Dog 객체 생성
        dog2.name = "Max";
        dog2.age = 5;

        dog1.birthday();  // dog1의 나이만 증가
        System.out.println(dog1.name + "의 나이: " + dog1.age); // 출력: Buddy의 나이: 4
        System.out.println(dog2.name + "의 나이: " + dog2.age); // 출력: Max의 나이: 5
    }
}
```
설명 : ```dog1```과 ```dog2```는 각각 ```Dog``` 클래스의 인스턴스이다.
```dog1```의 ```name```과 ```age```는 ```"Buddy"```와 ```3```으로 설정되며, ```dog2```의 ```name```과 ```age```는 ```"Max"```와 ```5```로 설정된다.
```dog1.birthday()``` 메소드는 ```dog1```의 ```age```만 증가시키며, ```dog2```의 ```age```는 변하지 않는다. 이처럼 인스턴스 필드는 객체마다 개별적으로 관리된다.

-------------------------
## 2. static이란.
static(정적) 키워드는 특정 필드나 메소드가 **모든 객체에서 공유**되어야 할 때 사용된다.<br>static 멤버는 클래스 로드 시 **한 번만 메모리에 할당**되며, 모든 객체가 동일한 메모리 공간을 참조하게 된다.

#### 2-1 static 필드와 메소드
**static** 필드는 클래스 전체에서 단 하나만 존재하며, 모든 객체가 이 필드에 접근할 때 동일한 값을 참조하고 공유한다.<br>**static 메소드**는 클래스에 속하며, 객체 없이도 호출할 수 있다. 인스턴스 필드나 인스턴스 메소드에 접근할 수 없고, 오직 **static필드와 static 메소드만을 사용할 수 있다**

##### 예제 : static필드와 static 메소드
```java
public class Counter {
    static int count = 0; // static 필드: 모든 Counter 객체가 공유하는 변수

    public Counter() {
        count++;  // 객체 생성 시 count 증가
    }

    static void displayCount() { // static 메소드
        System.out.println("현재 생성된 객체 수: " + count);
    }
}

public class Main {
    public static void main(String[] args) {
        Counter obj1 = new Counter(); // 첫 번째 Counter 객체 생성
        Counter obj2 = new Counter(); // 두 번째 Counter 객체 생성

        Counter.displayCount(); // 출력: 현재 생성된 객체 수: 2
    }
}
```
설명 : ```count```는 static 필드로 모든 ```Counter```객체에서 공유되며, 객체가 생성될 때마다 1씩 증가한다.<br>static 메소드 ```displayCount()```는 객체 생성 없이 ```Counter.displayCount()```로 호출할 수 있으며, 현재 생성된 객체 수를 출력한다.

--------------------------------
## 3. 인스턴스와 static의 차이점 요약
|비교 항목|인스턴스|static|
|:---|:----|:----|
|메모리 할당 시점|객체가 생성될 때마다 개별적으로 할당|클래스 로드 시 한 번만 할당|
|메모리 위치|힙(Heap) 메모리|메서드 영역(Method Area)|
|값의 독립성|각 객체마다 고유의 값을 가짐|모든 객체에서 하나의 값을 공유|
|접근 방식|객체 참조 변수(예:myCar.field)를 통해 접근|클래스 이름(예:Classname.field)를 통해 접근 가능, 객체를 통해서도 접근 가능|
|사용 목적|객체가 고유하게 가져야 하는 데이터나 동작|모든 객체가 공통으로 사용하는 데이터나 동작|
|초기화 시점|객체 생성 시점에서 초기화|클래스 로드 시점에서 초기화|
|대표적인 용도|개별 객체의 상태를 저장하는 필드나 동작 메소드 (예 : speed,color,accelerate())|모든 객체가 공유해야 하는 필드나 동작 메소드(예 : carCount,displayCarCount())|
|메소드 제약 사항|다른 인스턴스 멤버(필드,메소드)에 자유롭게 접근 가능|인스턴스 멤버에 접근할 수 없고, static 멤버만 접근 가능|

-----------------------
## 4. 인스턴스와 static 필드 및 메소드의 상호작용

##### 예제 : 인스턴스와 static 필드 간의 상호작용
```java
public class BankAccount {
    static double interestRate = 0.02;  // static 필드: 모든 계좌에 동일한 이자율 적용
    double balance;                     // 인스턴스 필드: 각 계좌의 잔액

    public BankAccount(double initialBalance) {
        balance = initialBalance;
    }

    void addInterest() {  // 인스턴스 메소드: 이자를 잔액에 추가
        balance += balance * interestRate;
    }

    static void setInterestRate(double newRate) { // static 메소드: 이자율 변경
        interestRate = newRate;
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount account1 = new BankAccount(1000);
        BankAccount account2 = new BankAccount(2000);

        account1.addInterest();  // 이자 추가
        System.out.println("Account1 잔액: " + account1.balance); // 출력: Account1 잔액: 1020.0

        BankAccount.setInterestRate(0.03); // 이자율을 3%로 변경

        account2.addInterest();
        System.out.println("Account2 잔액: " + account2.balance); // 출력: Account2 잔액: 2060.0
    }
}
```
설명 : ```interestRate```는 static 필드로 모든 ```BanckAccount```객체가 공유하며, 이자율이 변경되면 모든 계좌에 동일하게 적용된다.
<br>```balance```는 인스턴스 필드로 각 계좌가 고유의 잔액을 가진다.
<br>```addInterest()```는 인스턴스 메소드로, 각 계좌에 개별적으로 이자를 추가한다.
<br>```setInterestRate()```는 static 메소드로, 클래스 전체의 이자율을 변경할 수 있다.
