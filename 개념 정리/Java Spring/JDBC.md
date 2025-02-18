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
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```SLECT```,```INSERT```,```UPDATE```,```DELETE```와 같은 SQL 명령을 실행할 수 있다.<br>
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

