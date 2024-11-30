# Java 문자열 처리 심화 : String과 StringBuilder의 차이와 활용
자바에서 문자열을 다루는 방법은 여러 가지가 있지만, 가장 흔히 사용하는 클래스는 String과 StringBuilder이다. 이 두 클래스는 문자열을 저장하고 조작하는 방식에서 차이가 있으며, 성능과 메모리 관리 측면에서도 중요한 차이를 가진다. 

## 1. String 클래스

#### 1-1 String이란.
String 클래스는 자바에서 **불변(immutable)** 객체로 정의된다. 불변 객체란, 한 번 생성된 후에는 그 내용이 절대로 변경되지 않는 객체를 의미한다.
이러한 불변성은 문자열 데이터의 안정성을 제공하고, 문자열 객체의 공유를 가능하게 하며, 스레드 안정성을 보장하는데 유리하다.
+ 문자열 상수 풀(String Constant Pool)
  + 자바는 메모리 관리를 위해 ```문자열 상수 풀```이라는 특수한 메모리 영역을 제공한다. 동일한 내용의 문자열 리터럴이 여러 번 사용될 때마다 새로운 객체를 생성하지 않고, 상수 풀에 동일한 ```String``` 객체를 재사용한다.
    <br>예를 들어, ```"Hello"```라는 문자열 리터럴이 여러 곳에서 사용된다면, 자바는 매번 새로운 객체를 생성하지 않고, 상수 풀에서 기존의 ```"Hello"```문자열을 참조하여 메모리 사용을 최적화한다.

##### 예제 : 문자열 상수 풀과 불변성의 동작
```java
public class StringExample {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = "Hello"; // str1과 같은 객체를 참조
        String str3 = new String("Hello"); // 새 객체 생성

        System.out.println(str1 == str2); // 출력: true (같은 객체를 참조)
        System.out.println(str1 == str3); // 출력: false (다른 객체를 참조)
    }
}
```
설명 : ```str1```과 ```str2```는 같은 리터럴 ```"Hello"```로 초기화되어, 상수 풀에서 동일한 객체를 참조한다.<br>```str3```는 ```new```키워드를 사용하여 새로운 ```String```객체를 생성하므로, ```str1```과 ```str3```서로 다른 객체다.

----------------------------------------
#### 1-2 String의 불변성(Immutable)과 그 영향
String 객체가 불변이므로 문자열을 수정할 수 없으며, 문자열을 변경하려는 시도가 있을 때마다 새로운 객체가 생성된다.<br>이러한 동작은 메모리 관리 측면에서 단점이 될 수있지만, 특정 상황에서는 불변성이 큰 장점이 될 수 잇다.
+ 안정성 : 불변성으로 인해, ```String```객체를 여러 곳에서 참조하더라도 의도치 않은 데이터 손실,변경이 발생하지 않는다.
+ 성능 문제 : 문자열을 반복적으로 변경해야 하는 작업에서는 ```String```의 불변성이 성능 문제로 이어질 수 있다. 문자열이 변경될 때마다 새로운 객체가 생성되어 메모리를 많이 소모하게 되며, 이는 성능 저하의 원인이 된다.

##### 예제 : 문자열의 불변성으로 인한 객체 생성
```java
public class StringImmutabilityExample {
    public static void main(String[] args) {
        String str = "Java";
        str = str + " Programming"; // 새로운 String 객체가 생성됨
        System.out.println(str);
    }
}
```
설명 : 원하는 결과인 ```"Java Programming"```을 만들기 위해 원래의 ```"Java"```객체는 변경되지 않으며, 새로운 ```String```객체가 생성된다. ```str```이 새로운 객체를 참조하게 되며, **이전의 ```"Java"```객체는 그대로 유지된다.**

------------------------------------
#### 1-3 String 클래스의 주요 메소드와 활용 예시
```String```클래스는 다양한 메소드를 통해 문자열을 조작할 수 있도록 한다. 이 메소드들은 ```String```객체를 변경하는 것이 아니라, 새로운 ```String```객체를 반환하여 결과를 제공한다.
+ chatAt(int index) : 특정 인덱스에 있는 문자를 반환한다.
+ length() : 문자열의 길이를 반환한다.
+ subString(int beginIndex, int endIndex) : 문자열의 특정 범위를 반환한다.
+ toUpperCase(), toLowerCase() : 대문자 및 소문자로 변환된 새로운 문자열을 반환한다.
+ replace(CharSequence target, CharSequence replecement) : 문자열 내 특정 부분을 다른 문자열로 대체한 결과를 반환한다.
+ equals(Object obj) : 두 문자열의 내용을 비교하면 같으면 true를, 다르면 false를 반환한다.
+ split(String regex) : 주어진 정규 표현식에 따라 문자열을 분리하여 String 배열로 반환한다.

##### 예제 : String 메소드 활용
```java
public class StringMethodsExample {
    public static void main(String[] args) {
        String str = "Hello, World";

        System.out.println("길이: " + str.length());                // 출력: 12
        System.out.println("3번째 문자: " + str.charAt(2));         // 출력: l
        System.out.println("부분 문자열: " + str.substring(0, 5)); // 출력: Hello
        System.out.println("소문자 변환: " + str.toLowerCase());    // 출력: hello, world
        System.out.println("대문자 변환: " + str.toUpperCase());    // 출력: HELLO, WORLD
        System.out.println("World 대체: " + str.replace("World", "Java")); // 출력: Hello, Java
    }
}
```
설명 : ```charAt()``` 메소드는 특정 위치의 문자를 반환하고, ```replace()``` 메소드는 문자열의 특정 부분을 대체한 새로운 문자열을 반환한다. ```substring()```메소드는 문자열의 특정 구간을 잘라내어 반환한다. 이러한 메소드들은  ```String```객체를 수정하지 않고, 항상 새로운 ```String```객체를 반환한다.

-------------------------------
## 2. StringBuilder 클래스
#### 2-1 StringBuilder란.
**StringBuilder** 는 **가변(mutable)** 객체로 설계되어 있으며, 생성된 이후에도 문자열의 내용을 자유롭게 변경할 수 있다. 이 클래스는 문자열 조작이 빈번하게 일어나는 상황에서 특히 유용하다.
+ 가변성(Mutability)
  + ```StringBuilder```객체는 문자열의 내용이 변경될 때마다 새로운 객체를 생성하지 않고, 기존 객체를 수정하여 문자열을 추가하거나 삭제할 수 있다.<br>
  이를 통해 ```String```보다 효율적인 메모리 사용이 가능하며, 문자열 추가, 삭제, 삽입 작업이 자주 일어나는 경우 ```StringBuilder```가 적합하다.
+ 동적 버퍼 관리
  + ```StringBuilder```는 내부적으로 동적버퍼를 사용하여 문자열의 크기를 유동적으로 조절한다. 문자열이 추가되면서 버퍼가 부족해지면, 자동으로 버퍼의 크기를 늘려준다.<br> 이로 인해 메모리 낭비를 줄이고, 문자열을 여러 번 수정하는 경우에도 높은 성능을 유지할 수 있다.

##### 예제 : StringBuilder의 가변성
```java
public class StringBuilderExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");

        sb.append(" World");   // 문자열 추가
        System.out.println("append 후: " + sb);  // 출력: Hello World

        sb.insert(5, " Java");  // 특정 위치에 문자열 삽입
        System.out.println("삽입 후: " + sb);  // 출력: Hello Java World

        sb.delete(5, 10);  // 특정 범위의 문자열 삭제
        System.out.println("삭제 후: " + sb);  // 출력: Hello World
    }
}
```
설명 : ```StringBuilder```객체 ```sb```는 ```"Hello"```라는 문자열로 초기화된다.<br>```append()```,```insert()```,```delete()``` 메소드를 통해 문자열을 조작할 때마다 **기존 객체가 수정**되므로 새로운 객체가 생성되지 않는다. 이는 메모리 효율성을 크게 향상시킨다.

--------------------------
#### 2-2 StringBuilder의 주요 메소드와 활용 예시
```StringBuilder```클래스는 다양한 메소드를 제공하여 문자열을 효율적으로 조작할 수 있다.
+ append(String str) : 문자열의 끝에 다른 문자열을 추가한다.
+ insert(int offset, String str) : 특정 인덱스에 문자열을 삽입한다.
+ delete(int start, int end) : 특정 범위의 문자열을 삭제한다.
+ reverse() : 문자열을 반대로 뒤집는다.
+ toString() : ```StringBuilder```의 문자열을 ```String```객체로 변환하여 반환한다.

##### 예제 : StringBuilder 메소드 활용
```java
public class StringBuilderMethodsExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Java");

        sb.append(" Programming");  // 문자열 추가
        System.out.println("append 후: " + sb);  // 출력: Java Programming

        sb.reverse();  // 문자열 뒤집기
        System.out.println("reverse 후: " + sb); // 출력: gnimmargorP avaJ

        sb.delete(0, 5);  // 특정 범위 삭제
        System.out.println("delete 후: " + sb);  // 출력: margorP avaJ
    }
}
```
설명 : ```append()``` 메소드는 문자열 끝에 다른 문자열을 추가하여 수정하고, ```reverse()```는 문자열을 뒤집어 반환하고, ```delete()``` 메소드를 사용하여 특정 인덱스 범위의 문자열을 삭제할 수 있다.

----------------------------------
## String과 StringBuilder의 성능 비교
