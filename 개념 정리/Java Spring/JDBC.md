## JDBC 개념
JDBC(Java Database Connectivity)는 **Java 애플리케이션과 관계형 데이터베이스(RDBMS)** 연결하여 데이터를 주고받을 수 있도록 해주는 표준 API이다. JDBC는 데이터베이스와 직접적으로 상호작용하는 매커니즘을 제공하여,
Java 프로그램이 MySQL, Oracle, PostgreSQL, SQL Servcer 등의 다양한 데이터베이스에서 데이터를 저장, 수정, 삭제 및 조회할 수 있도록 도와준다.

애플리케이션을 개발할 때, 데이터를 저장하고 관리하는 것은 필수적인 요소이다. 일반적으로 데이터를 저장하는 곳은 데이터베이스이며, JDBC는 이 데이터베이스와 Java 애플리케이션이 원활하게 소통할 수 있도록 연결을 담당한다.

예를 들어 회원 관리 시스템을 개발한다고 가정해보자. 사용자가 회원가입을 하면, 입력한 정보(이름, 이메일, 비밀번호 등)는 데이터베이스에 저장되어야 한다. 또한, 사용자가 로그인하면 데이터베이스에서 정보를 가져와 검증해야 한다.
이러한 과정이 가능하도록 **JDBC가 애플리케이션과 데이터베이스 사이의 다리 역할**을 한다.

--------------
## JDBC 역할
JDBC는 Java 프로그램과 데이터베이스를 연결하는 중간 계층으로서, 다음과 같은 역할을 수행한다.

**데이터베이스 연결(Database Connection)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JDBC는 Java 애플리케이션이 데이터베이스에 연결할 수 있도록 지원한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터베이스에 연결하면, SQL 문을 실행할 수 있으며, 데이터를 읽고 쓸 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```DriverManager```를 사용하여 데이터베이스와 연결을 생성한다.

**SQL 실행(SQL Execution)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터베이스에서 데이터를 조작하기 위해 SQL 문을 실행할 수 있도록 지원한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```SELECT```,```INSERT```,```UPDATE```,```DELETE```와 같은 SQL 명령을 실행할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```Statement```,```PreparedStatement```,```CallableStatement``` 등의 객체를 사용하여 SQL을 실행한다.

**결과 처리(Result Processing)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SQL 문을 실행한 후, 반환된 데이터를 ```ResultSet```객체를 통해 Java에서 활용할 수 있도록 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;결과 데이터를 Java 변수나 객체로 변환하여 사용할 수 있도록 지원한다.

**트랜잭션 관리(Transaction Management)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;여러 개의 SQL 문을 하나의 논리적인 작업 단위로 묶어 처리할 수 있도록 지원한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```commit()```,```rollback()```을 활용하여 데이터의 일관성과 무결성을 유지할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, 계좌 이체와 같은 작업에서 돈을 인출하는 SQL문과 입금하는 SQL문이 함께 성공해야 하므로 트랜잭션이 필요하다.

**리소스 관리(Resource Management)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터베이스와의 연결을 종료하고 사용했던 리소스를 해제하여 성능 저하 및 메모리 누수를 방지한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```close()```메서드를 이용하여 ```Connection```,```Statement```,```ResultSet```등의 객체를 명시적으로 해제해야 한다.

---------------
## JDBC의 동작 과정
JDBC를 사용하여 데이터베이스와 상호작용하는 과정은 여섯 단계로 나뉜다.

**JDBC 드라이버 로드(Load JDBC Driver)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JDBC 드라이버를 로드하여 Java 애플리케이션이 데이터베이스와 통신할 수 있도록 준비한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;최신 JDBC 버전에서는 자동 로딩이 가능하지만, 필요할 경우 ```Class.forName("com.mysql.cj.jdbc.Driver")```를 사용하여 명시적으로도 로드할 수도 있다.

**데이터베이스 연결(Eatablish Connection)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```DriverManager```를 사용하여 데이터베이스와 연결하고, ```Connection```객체를 생성한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, MySQL 데이터베이스와 연결하려면 다음과 같은 코드가 필요하다.<br>
```java
Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/sampledb", "root", "password");
```

**SQL문 실행(Execute SQL Statement)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SQL문 실행 결과를 ```ResultSet```객체를 통해 가져오고, 데이터를 Java에서 사용할 수 있도록 가공한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, ```getString()```,```getInt()``` 등의 메서드를 사용하여 결과를 Java변수로 변환할 수 있다.<br>

**트랜잭션 관리(Transaction Management)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```setAutoCommit(false)```를 설정하여 자동 커밋을 비활성화한 후, 여러 개의 SQL문을 실행한 뒤 ```commit()``` 또는 ```rollback()```을 수행할 수 있다.

**리소스 해제(Close Resources)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 연결을 종료하고, 사용했던 ```Statement```와 ```ResultSet``` 객체를 닫아 시스템 자원을 절약한다.

------------------
## JDBC의 기본 코드 예제
JDBC를 이용하여 데이터베이스와 연결하고, 데이터를 조회하는 기본적인 코드이다.\
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class JdbcExample {
    public static void main(String[] args) {
        // 데이터베이스 연결 정보
        String url = "jdbc:mysql://localhost:3306/sampledb";
        String user = "root";
        String password = "password";

        // JDBC 객체 선언
        Connection conn = null;
        Statement stmt = null;
        ResultSet rs = null;

        try {
            // 1. 데이터베이스 연결
            conn = DriverManager.getConnection(url, user, password);
            System.out.println("데이터베이스에 연결되었습니다.");

            // 2. SQL 실행
            stmt = conn.createStatement();
            String sql = "SELECT id, name FROM users";
            rs = stmt.executeQuery(sql);

            // 3. 결과 처리
            while (rs.next()) {
                int id = rs.getInt("id");
                String name = rs.getString("name");
                System.out.println("ID: " + id + ", Name: " + name);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            // 4. 리소스 해제
            try {
                if (rs != null) rs.close();
                if (stmt != null) stmt.close();
                if (conn != null) conn.close();
                System.out.println("데이터베이스 연결이 종료되었습니다.");
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```
---------------
## JDBC의 장단점
장점
+ **표준 API 제공** : 다양한 데이터베이스와의 호환성을 갖춘 일관된 인터페이스 제공
+ **SQL 직접 제어 가능** : SQL을 직접 실행하여 세밀한 데이터 조작이 가능함
+ **트랜잭션 관리 지원** : ```commit()``` 및 ```rollback()```을 통해 데이터의 일관성 유지 기능

단점
+ **SQL 의존성** : 데이터베이스별 SQL 문법 차이로 인해 코드 변경이 필요할 수 있음
+ **코드 복잡성** : ```Connection```,```Statement```,```ResultSet``` 등을 직접 관리해야 하므로 코드가 길어질 수 있음
+ **생상성 저하** : Spring JDBC, JPA와 같은 고수준 API에 비해 코드량이 많고 유지보수가 어렵다.

## JDBC의 특징
### JDBC의 플랫폼 독립성
JDBC는 Java의 핵심 철학인 "Write Once, Run Anywhere"를 데이터베이스 연동 부분에서도 실현할 수 있도록 한다. 플랫폼 독립성이란 한 번 작성한 코드가 **운영 체제(OS)나 데이터베이스의 종류에 관계없이 동일하게 동작**하게
할 수 있도록 보장하는 것을 의미한다.

Java는 운영 체제에 의존하지 않고 JVM(Java Virtual Machine) 위에서 실행된다. 따라서 Java로 작성된 애플리케이션은 Windows, maxOS, Linux 등 다양한 환경에서 동일하게 동작한다.
JDBC도 이와 같은 원리로 **하나의 표준 인터페이스** 를 제공하여 MySQL, Oracle, PostgreSQL, SQL Server 등 다양한 데이터베이스와 동일한 방식으로 연결하고 SQL를 실행할 수 있도록 한다.

하지만 데이터베이스마다 세부적인 SQL 문법이 다를 수 있기 때문에, 완전한 플랫폼 독립성을 보장하기 위해서는 JDBC 드라이버가 필요하다. JDBC 드라이버는 데이터베이스마다 제공되는 별도의 라이브러리로,JDBC API를 해당 데이터베이스의 네이티브 명령어로 변환하는 역할을 한다. 즉, 애플리케이션에는 JDBC API만 신경 쓰면 되고 DBMS에 따라 드라이버만 변경해주면 동일한 코드가 여러 데이터베이스에서 동작할 수 있다.

## JDBC의 플랫폼 독립성을 가능하게 하는 요소
**JDBC API(Java Application -> JDBC API)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Java에서 데이터베이스를 제어할 수 있도록 표준화된 API<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```java.sql```패키지에 포함된 인터페이스와 클래스를 제공<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```Connection```,```Statement```,```PreparedStatement```,```ResultSet```등의 객체를 활용하여 데이터베이스와 상호작용

**JDBC 드라이버(JDBC API -> JDBC Driver)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JDBC API 호출을 데이터베이스가 이해할 수 있는 네이티브 코드로 변환<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;DBMS마다 다른 JDBC 드라이버를 사용하지만, 코드 변경없이 드라이버만 교체하면 동일한 Java 코드로 다양한 데이터베이스와 연결 가능<br>

**DBMS(JDBC Driver -> Database)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;변환된 SQL 명령을 실행하여 데이터를 처리하고 결과를 반환

### JDBC의 플랫폼 독립성 에제
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class JdbcPlatformIndependence {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/sampledb";
        String user = "root";
        String password = "password";

        try {
            // JDBC 드라이버를 통해 데이터베이스에 연결
            Connection conn = DriverManager.getConnection(url, user, password);
            System.out.println("데이터베이스 연결 성공!");

            // 연결 종료
            conn.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```
위의 코드에서 url, user, password 정보만 변경하면 Oracle, PostrgerSQL, SQL Server 등의 데이터베이스에서도 동일한 코드로 실행가능하다. 즉, JDBC API는 변경되지 않고, 데이터베이스에 맞는 JDBC 드라이버만 변경해주면
다른 환경에서도 동일하게 동작할 수 있다.

예를 들어, MySQL에서 Oracle로 변경하려면 JDBC URL과 드라이버 설정만 변경하면 된다.
```java
String url = "jdbc:oracle:thin:@localhost:1521:orcl";
String user = "oracle_user";
String password = "oracle_password";
```

---------------------
## JDBC의 SQL 실행 지원
JDBC의 핵심 기능 중 하나는 SQL 문을 실행하여 데이터베이스와 상호작용하는 것이다. JDBC를 활용하면 다음과 같은 SQL 문을 실행할 수 있다.

**SELECT(데이터 조회)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터베이스에서 데이터를 검색하는 기능<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```executeQuery()```를 통해 실행

**INSERT(데이터 삽입)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;새로운 데이터를 추가하는 기능<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```executeUpdate()```를 통해 실행

**UPDATE(데이터 수정)** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;기존 데이터를 수정하는 기능<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```executeUpdate()```를 통해 실행

**DELETE(데이터 삭제)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터를 삭제하는 기능<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```executeUpdate()```를 통해 실행

예제
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class JdbcSqlExecution {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/sampledb";
        String user = "root";
        String password = "password";

        Connection conn = null;
        Statement stmt = null;

        try {
            // 데이터베이스 연결
            conn = DriverManager.getConnection(url, user, password);
            stmt = conn.createStatement();

            // INSERT 문 실행
            String insertSql = "INSERT INTO users (name, email) VALUES ('홍길동', 'hong@example.com')";
            int rowsInserted = stmt.executeUpdate(insertSql);
            System.out.println(rowsInserted + "개의 행이 추가되었습니다.");

            // UPDATE 문 실행
            String updateSql = "UPDATE users SET email = 'gil@example.com' WHERE name = '홍길동'";
            int rowsUpdated = stmt.executeUpdate(updateSql);
            System.out.println(rowsUpdated + "개의 행이 수정되었습니다.");

            // DELETE 문 실행
            String deleteSql = "DELETE FROM users WHERE name = '홍길동'";
            int rowsDeleted = stmt.executeUpdate(deleteSql);
            System.out.println(rowsDeleted + "개의 행이 삭제되었습니다.");
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            // 리소스 해제
            try {
                if (stmt != null) stmt.close();
                if (conn != null) conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```
-------
## JDBC 트랜잭션 관리
JDBC는 데이터의 일관성을 유지하기 위해 트랜잭션(Transaction) 관리 기능을 제공한다. 트랜잭션은 **하나의 논리적인 작업 단위** 로, 여러 개의 SQL 문을 하나의 작업으로 묶어 실행할 수 있다.

JDBC에서 기본적으로 **자동 커밋(Auto Commit)** 이 활성화되어 있다. 즉, SQL문이 실행될 때마다 자동으로 데이터베이스에 적용된다. 하지만, 이를 비활성화하고 수동으로 ```commit()```과 ```rollback()```을 조작할 수도있다.

예제
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class JdbcTransactionManagement {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/sampledb";
        String user = "root";
        String password = "password";

        Connection conn = null;
        Statement stmt = null;

        try {
            conn = DriverManager.getConnection(url, user, password);
            conn.setAutoCommit(false); // 자동 커밋 비활성화

            stmt = conn.createStatement();
            stmt.executeUpdate("INSERT INTO accounts (name, balance) VALUES ('김철수', 50000)");
            stmt.executeUpdate("INSERT INTO accounts (name, balance) VALUES ('이영희', 60000)");

            // 일부러 오류 발생시키기
            int result = 10 / 0; // ArithmeticException 발생

            conn.commit(); // 트랜잭션 커밋
        } catch (Exception e) {
            try {
                if (conn != null) conn.rollback(); // 오류 발생 시 롤백
            } catch (SQLException rollbackEx) {
                rollbackEx.printStackTrace();
            }
            e.printStackTrace();
        } finally {
            try {
                if (stmt != null) stmt.close();
                if (conn != null) conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```
-----------
## JDBC 드라이버의 개념
JDBC 드라이버는 JDBC API와 데이터베이스(DBMS) 간의 중재자 역할을 하는 프로그램이다.<br>
애플리케이션이 데이터베이스와 통신하려면 SQL을 데이터베이스가 이해할 수 있는 형태로 변환해야 하며, 반대로 데이터베이스에서 반환된 결과를 Java 애플리케이션이 이해할 수 있도록 변환해야 한다.<br>
JDBC 드라이버는 이러한 변환 과정을 담당하는 소프트웨어 계층으로, JDBC API를 통해 전달된 SQL 명령을 적절한 방식으로 DBMS에 전달하고, DBMS의 응답을 Java 애플리케이션이 처리할 수 있도록 변환하는 역할을 한다.

### JDBC 드라이버의 역할
**JDBC API의 SQL 명령을 DBMS에서 이해할 수 있도록 변환**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Java 애플리케이션에서 작성된 ```SELECT```,```INSERT```,```UPDATE```,```DELETE``` 등의 SQL 문을 데이터베이스가 이해할 수 있는 형태로 변환하여 전달한다.

**DBMS의 응답을 Java에서 사용할 수 있도록 변환**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터베이스에서 실행된 결과를 ResultSet 객체로 변환하여 Java 애플리케이션이 처리할 수 있도록 한다.

**DBMS와의 연결을 관리** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JDBC 드라이버는 Java 애플리케이션과 데이터베이스 간의 연결을 생성하고, 유지하며, 종료하는 역할을 한다.

**트랜잭션 관리 지원**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JDBC 드라이버는 ```commit()```와 ```rollback()```을 처리하여 데이터의 일관성을 유지하는 트랜잭션 관리를 지원한다.

**데이터베이스의 네트워크 통신 처리**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JDBC 드라이버는 데이터베이스 서버와의 네트워크 연결을 관리하며, 클라이언트와 서버 간의 데이터 전송을 수행한다.

### JDBC 드라이버의 동작 과정
-> Java 애플리케이션이 JDBC API를 통해 데이터베이스 연결을 요청한다.<br>
-> JDBC 드라이버가 해당 요청을 받아 데이터베이스에 적절한 명령을 전달한다.<br>
-> 데이터베이스가 SQL 문을 실행하고 결과를 생성한다.<br>
-> JDBC 드라이버가 실행 결과를 변환하여 Java 애플리케이션으로 반환한다.<br>
-> 애플리케이션이 반환된 데이터를 처리하고, 필요하면 트랜잭션을 관리한다.
```java
Java 애플리케이션
    │
    ├──> JDBC API
    │       │
    │       ├──> JDBC 드라이버
    │       │       │
    │       │       ├──> 데이터베이스 (SQL 실행)
    │       │       │
    │       │       └──> SQL 실행 결과 반환
    │       │
    │       └──> Java 애플리케이션 (결과 처리)
```
예제 : JDBC 드라이버를 활용한 기본 데이터베이스 연결
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class JdbcDriverExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/sampledb";
        String user = "root";
        String password = "password";

        Connection conn = null;

        try {
            // JDBC 드라이버를 통해 데이터베이스에 연결
            conn = DriverManager.getConnection(url, user, password);
            System.out.println("데이터베이스 연결 성공!");
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            try {
                if (conn != null) {
                    conn.close();
                    System.out.println("데이터베이스 연결 종료.");
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```
## JDBC 드라이버의 필요성
**SQL문 실행의 표준화**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; JDBC API는 Java 애플리케이션에서 일관된 방식으로 SQL문을 실행할 수 있도록 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, MySQL과 Oracle의 SQL 문법이 다를 수 있지만, JDBC API를 활용하면 동일한 코드로 데이터를 조회하거나 수정할 수 있다.

**DBMS에 대한 의존성 최소화**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터베이스가 변경되더라도, JDBC API를 사용하면 코드를 최소한으로 수정하여 재사용할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, MySQL에서 PostgreSQL로 변경할 경우, JDBC URL과 드라이버만 교체하면 된다.

**운영 체제와 독립적으로 동작**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JDBC는 Java기반이므로 운영체제(OS)와 무관하게 동일한 방식으로 동작한다.

---------------
### JDBC 드라이버의 라이브러리 형태
JDBC 드라이버는 보통 JAR(Java Archive)파일 형태로 제공된다.<br>
JAR 파일을 프로젝트에 추가하면 JDBC 드라이버를 사용할 수 있다.

|데이터베이스|JDBC 드라이버 파일명|
|:---|:---|
| MySQL | mysql-connector-java-8.0.26.jar |
| Oracle | ojdbc8.jar |
| PostgreSQL | postgresql-42.2.23.jar |
| SQL Server | mssql-jdbc-9.4.0.jre8.jar | 

## JDBC 드라이버의 종류
JDBC 드라이버는 내부 구현 방식에 따라 네 가지 유형으로 분류된다. 각 드라이버는 성능, 플랫폼 독립성, 데이터베이스 종속성 등의 특성이 다르므로, 프로젝트의 특성과 환경에 따라 적절한 드라이버를 선택하는것이 중요하다.

### JDBC 드라이버의 네 가지 유형
+ Type 1 : JDBC-ODBC 브리지 드라이버
+ Type 2 : 네이티브 API 드라이버
+ Type 3 : 네트워크 프로토콜 드라이버
+ Type 4 : 순수 Java 드라이버(Thin 드라이버)

---------------------------
### Type 1 : JDBC-ODBC 브리지 드라이버
JDBC-ODBC 드라이버는 가장 오래된 JDBC 드라이버 유형으로, ODBC(Open Database Connectivity)드라이버를 이용해 Java 애플리케이션과 데이터베이스를 연결한다.

**작동 방식**<br>
-> JDBC API 호출을 받으면 JDBC-ODBC 브리지 드라이버가 ODBC API로 변환한다.<br>
-> ODBC API는 다시 DBMS의 네이티브 드라이버를 호출하여 데이터베이스와 통신한다.<br>
-> 데이터베이스의 응답이 같은 경로를 통해 Java 애플리케이션으로 반환된다.

**장점**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 다양한 데이터베이스와 호환 가능<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 기존 ODBC 드라이버가 있다면 드라이버 설치 없이 사용 가능

**단점**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 성능이 가장 낮음(JDBC -> ODBC -> 네이티브 드라이버를 거쳐야 하므로 오버헤드가 크다)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 네이티브 코드가 포함되어 있어 플랫폼 독립성이 떨어짐<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 최신 Java 버전에서는 더 이상 지원되지 않음

**사용 예제**
```java
String url = "jdbc:odbc:DataSourceName";
Connection conn = DriverManager.getConnection(url, "user", "password");
```

**비고**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Type 1 드라이버는 현재 실무에서 거의 사용되지 않으며, Java 8 이후부터는 공식적으로 지원되지 않는다.

---------------
### Type 2 : 네이티브 API 드라이버
특정 데이터베이스의 네이티브 API를 직접 호출하는 방식으로 동작한다. 데이터베이스 공급업체가 제공하는 클라이언트 라이브러리를 필요로 하며, 해당 라이브러리가 운영 체제에 설치되어 있어야 한다.

**작동 방식**<br>
-> Java 애플리케이션에서 JDBC API를 호출한다.<br>
-> JDBC API가 네이티브 API로 변환된다.
-> 네이티브 API가 데이터베이스와 직업 통신하여 SQL 명령을 실행한다.
-> 결과가 Java 애플리케이션으로 반환된다.

**장점**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Type 1 보다 성능이 뛰어남<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터베이스의 네이티비 기능을 활용할 수 있음

**단점**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;특정 데이터베이스에 종속됨(MySQL, Oracle, MSSQL 등 데이터베이스별로 다른 드라이버 필요)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;네이티브 라이브러리를 운영체제에 설치해야 함(운영체제 의존성이 있음)

**사용 예제**
```java
String url = "jdbc:oracle:thin:@localhost:1521:xe";
Connection conn = DriverManager.getConnection(url, "user", "password");
```

**비고**<br>
네이티브 API를 직접 활용하는 방식이므로 Type 1보다는 빠르지만, 설치와 유지보수가 까다롭다는 단점이 있다.

----------------
### Type 3 : 네트워크 프로토콜 드라이버
이 드라이버는 클라이언트와 데이터베이스 사이에 미들웨어 서버를 두고 네트워크 프로토콜을 사용하여 통신하는 방식이다. JDBC API호출을 네트워크 프로토콜로 변환하여 미들웨어 서버로 전송하고, 미들웨어 서버가
이를 다시  데이터베이스의 네이티브 프로토콜로 변환하여 실행하는 구조다.

**작동 방식**<br>
-> Java 애플리케이션에서 JDBC API를 호출한다.<br>
-> Type 3 드라이버가 JDBC API를 네트워크 프로토콜로 변환하여 미들웨어 서버로 전송한다.<br>
-> 미들웨어 서버가 네트워크 프로토콜을 데이터베이스의 네이티브 API로 변환하여 실행한다.<br>
-> 실행 결과를 같은 경로를 거쳐 Java 애플리케이션으로 변환한다.

**장점**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트 측에 데이터베이스별 드라이버 설치가 필요 없음(미들웨어 서버가 모든 드라이버를 관리)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;여러 데이터베이스를 동시에 지원할 수 있음<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;방화벽을 통해 데이터베이스와 쉽게 연결 가능

**단점**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;미들웨어 서버를 별도로 운영해야 하므로 추가적인 인프라가 필요함<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;미들웨어 서버를 거치는 과정에서 성능 저하 발생 가능

**사용 예제**
```java
String url = "jdbc:networkprotocol://middleware-server:1521/db";
Connection conn = DriverManager.getConnection(url, "user", "password");
```

**비고**<br>
클라이언트-서버 환경에서 유용하지만, 미들웨어 서버의 추가 비용과 관리 부담이 크다.

------------
### Type 4 : 순수 Java 드라이버 (Thin 드라이버)
이 드라이버는 Pure Java로 구현된 JDBC 드라이버로, 네이티브 코드 없이 직접 데이터베이스와 통신하는 방식이다. 네트워크 소켓을 통해 데이터베이스의 프로토콜을 직접 처리하기 떄문에 가장 많이 사용되는 방식이다.

**작동 방식**<br>
-> Java 애플리케이션에서 JDBC API를 호출한다.<br>
-> Type 4 드라이버가 네트워크 소켓을 통해 SQL를 데이터베이스에 전달한다.<br>
-> 데이터베이스가 SQL를 실행한 후 결과를 반환한다.<br>
-> Type 4 드라이버가 데이터를 Java 애플리케이션이 이해할 수 있는 형태로 변환하여 반환한다.

**장점**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;가장 빠른 성능(중간 계층이 없어 직접 DBMS와 통신)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;운영체제 독립적(Pure Java로 구현되어 있어 어떤 OS에서도 실행 가능)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트 측에 추가적인 네이티브 드라이버 설치가 필요 없음<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;네트워크를 통해 원격 데이터베이스와 쉽게 연결 가능

**단점**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 별로 다른 드라이버가 필요함

**사용 예제**
```java
String url = "jdbc:mysql://localhost:3306/sampledb";
Connection conn = DriverManager.getConnection(url, "user", "password");
```

**비고**<br>
Type 4 드라이버는 현재 가장 널리 사용되는 JDBC 드라이버 유형이며, 대부분의 Java 애플리케이션에서 사용된다.

|드라이버 유형|설명|
|:---|:---|
|Type 1|JDBC-ODBC 브리지 드라이버, ODBC를 사용하여 데이터베이스와 연결|
|Type 2|네이티브 API 드라이버, DBMS의 네이티브 코드 호출|
|Type 3|네트워크 프로토콜 드라이버, 미들웨어 서버를 경유하여 연결|
|Type 4|순수 Java 드라이버, 데이터베이스에 직접 연결|

------------
## JDBC 환경 설정
JDBC 드라이버를 설정하는 과정은 Java 애플리케이션에서 데이터베이스에 접근하기 위한 필수적인 절차이다. 올바른 JDBC 드라이버를 설정하지 않으면 데이터베이스 연결이 불가능하므로, 프로젝트에 적절한 드라이버를 추가하고,
올바르게 설정하는 방법을 정확히 이해하는 것이 중요하다.

### JDBC 드라이버 다운로드 및 설치
공식 홈페이지를 통해 설치하거나, Maven 또는 Gradle을 사용한 자동설치가 존재한다.<br>
프로젝트에서 Maven 또는 Gradle을 사용하면, 직접 파일을 다운로드 하지 않고도 라이브러리를 관리할 수 있다.

Maven 설정 예제(pom.xml파일에 추가)
```java
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.33</version>
</dependency>
```
Gradle 설정 예제(build.gradle 파일에 추가)
```java
dependencies {
    implementation 'mysql:mysql-connector-java:8.0.33'
}
```
-----------
### JDBC 드라이버 로드하기
JDBC 드라이버를 올바르게 설정한 후, 애플리케이션에서 드라이버를 로드하는 과정이 필요하다.JDBC 드라이버는 ```java.sql.DriverManager```클래스를 사용하여 등록된다.

Class.forName()을 사용한 드라이버 로드
```java
Class.forName("com.mysql.cj.jdbc.Driver");
```
위 코드가 실행되면 JDBC 드라이버 클래스가 로드되고, 해당 드라이버가 DriverManager에 등록된다.<br>
그러나 JDBC 4.0 이후부터는 명시적인 드라이버 로드가 필요하지 않다.

최신 JDBC 드라이버는 자동으로 ```DriverManager```에 등록되므로, Class.forName() 호출이 불필요하다.<br>
즉, 단순히 데이터베이스 연결 코드만 작성하면 드라이버가 자동으로 드한다.

-------------
### JDBC 드라이버 연결 테스트
JDBC 드ㅏ이버가 정상적으로 설정되었는지 확인하려면, ```DriverManager.getConnetion()```을 사용하여 데이터베이스에 직접 연결해볼 수 있다.
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class JdbcTest {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/sampledb";
        String user = "root";
        String password = "password";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            if (conn != null) {
                System.out.println("데이터베이스 연결 성공!");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### JDBC 드라이버 설징 시 주의할 점
**JDBC URL의 올바른 설정**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MySQL:```jdbc:mysql://localhost:3306/sampledb```<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PostgreSQL```: jdbc:postgresql://localhost:5432/sampledb```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Oracle: ```jdbc:oracle:thin:@localhost:1521:xe```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MSSQL: ```jdbc:sqlserver://localhost:1433;databaseName=sampledb```

**방화벽 및 포트 확인**<br>
MySQL 기본포트는 ```3306```, PostgreSQL은 ```5432```, MSSQL은 ```1433``` 이다.

-------------------
## Java 프로젝트에서 JDBC 사용 준비
JDBC를 활용하려면 프로젝트에서 필요한 설정을 완료해야 한다. 단순히 JDBC 드라이버를 추가하는것만으로는 충분하지 않으며, 올바른 패키지 구성, 연결 관리 방법, 예외 처리 방식 등을 고려해야 한다.

### 프로젝트 설정 방법
**Maven 프로젝트에서 설정**<br>
MySQL 드라이버 추가(pom.xml)
```java
<dependencies>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.33</version>
    </dependency>
</dependencies>
```
PostgreSQL 드라이버 추가(pom.xml)
```java
<dependencies>
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
        <version>42.5.0</version>
    </dependency>
</dependencies>
```
### 데이터베이스 연결 정보 구성
JDBC를 사용하여 데이터베이스에 접근하려면 데이터베이스의 연결 정보를 관리해야 한다. 일반적으로 다음 정보가 필요하다
+ JDBC URL : 데이터베이스에 접근하기 위한 주소
+ 사용자명(username) : 데이터베이스 로그인 계정
+ 비밀번호(password) : 해당 계정의 비밀번호

```java
jdbc.url=jdbc:mysql://localhost:3306/sampledb
jdbc.username=root
jdbc.password=password
```
### 프로젝트 구조
JDBC를 사용하는 Java 프로젝트는 기본적으로 다음과 같은 구조를 가지는 것이 일반적이다.
```java
/src
  /main
    /java
      /com/example
        /config
          DatabaseConfig.java  <-- 데이터베이스 설정 클래스
        /dao
          UserDao.java         <-- 데이터 액세스 객체 (DAO)
        /model
          User.java            <-- 엔티티 클래스
        /service
          UserService.java     <-- 비즈니스 로직
    /resources
      db.properties            <-- DB 연결 정보 저장
```
이러한 구조를 가지면 데이터베이스 연결 설정과 실제 데이터 접근 로직을 분리할 수 있어 유지보수가 용이하다.

### 데이터베이스 연결을 위한 설정 클래스 작성
JDBC를 사용할 때 데이터베이스 연결 설정을 별도의 클래스로 분리하면 코드의 재사용성과 유지보수성이 향상된다.
```java
package com.example.config;

import java.io.FileInputStream;
import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.util.Properties;

public class DatabaseConfig {
    private static final String PROPERTIES_FILE = "src/main/resources/db.properties";

    public static Connection getConnection() throws SQLException, IOException {
        Properties properties = new Properties();
        properties.load(new FileInputStream(PROPERTIES_FILE));

        String url = properties.getProperty("jdbc.url");
        String user = properties.getProperty("jdbc.username");
        String password = properties.getProperty("jdbc.password");

        return DriverManager.getConnection(url, user, password);
    }
}
```

### 데이터 액세스 개체 (DAO) 패턴 적용
JDBC를 사용할 때 직접 SQL을 실행하는 대신, 데이터베이스 접근을 담당하는 DAO(Date Access Object)패턴을 적용하면 코드가 더 쳬게적으로 관리될 수 있다.
```java
package com.example.dao;

import com.example.config.DatabaseConfig;
import com.example.model.User;

import java.io.IOException;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class UserDao {
    private static final String SELECT_USER_BY_ID = "SELECT id, name, email FROM users WHERE id = ?";

    public User getUserById(int id) {
        try (Connection conn = DatabaseConfig.getConnection();
             PreparedStatement pstmt = conn.prepareStatement(SELECT_USER_BY_ID)) {

            pstmt.setInt(1, id);
            ResultSet rs = pstmt.executeQuery();

            if (rs.next()) {
                return new User(rs.getInt("id"), rs.getString("name"), rs.getString("email"));
            }
        } catch (SQLException | IOException e) {
            e.printStackTrace();
        }
        return null;
    }
}
```

### JDBC 예외 처리 전략
JDBC를 사용할 때 발생할 수 있는 대표적인 예외들은 다음과 같다.
+ ClassNotFoundException : JDBC 드라이버가 로드되지 않은 경우 발생
+ SQLException : SQL 실행 중 오류 발생 (잘못된 쿼리,DB 연결 실패 등)
+ IOException : 설정 파일(db.properties)를 읽는 도중 문제가 발생한 경우
```java
try {
    Connection conn = DatabaseConfig.getConnection();
    System.out.println("DB 연결 성공!");
} catch (SQLException e) {
    System.out.println("SQL 오류: " + e.getMessage());
    e.printStackTrace();
} catch (IOException e) {
    System.out.println("설정 파일 로드 실패: " + e.getMessage());
}
```
-------------------
## 데이터베이스 연결
JDBC를 이용해 데이터베이스를 연결하려면 ```DriverManager``` 클래스를 사용해야 한다. ```DriverManager```는 데이터베이스와의 연결을 관리하는 역할을 수행하며, 다양한 DBMS와 상호작용할 수 있도록 지원한다.

### DriverManager의 역할
DriverManager는 JDBC 드라이버를 로드하고, 애플리케이션과 DB 사이의 연결을 설정하는 역할을 한다.

-> JDBC 드라이버 로드<br>
-> 데이터베이스 연결 생성<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;DriverManager.getConnection(String url, String user, String password)를 사용하여 DB와 연결한다.<br>
-> 연결된 드라이버 관리<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;getConnection()이 호출되면 등록된 JDBC 드라이버 목록을 확인하고, 적절한 드라이버를 선택하여 연결을 수행한다.

### JDBC URL 구성 방식
JDBC URL은 데이터베이스에 접근하기 위한 문자열로, 특정한 형식을 따른다. 기본 구조는 다음과 같다.
```java
jdbc:[DBMS]://[호스트]:[포트]/[데이터베이스명]
```
MySQL
```java
jdbc:mysql://localhost:3306/sampledb
```
PostgreSQL
```java
jdbc:postgresql://localhost:5432/sampledb
```
Oracle
```java
jdbc:oracle:thin:@localhost:1521:xe
```
