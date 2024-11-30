## 1. 버퍼(Buffer)의 개념과 중요성
Java에서 **Buffer**는 메모리 상의 특정 영역으로, 입출력 작업의 속도의 효율을 높이기 위해 데이터의 임시 저장소 역할을 한다.    
버퍼는 데이터를 처리할 때 데이터의 전송 효율을 높이고, **CPU와 입출력 장치 간의 속도 차이를 보완**하는 중요한 기능을 제공한다.

#### 1-1 버퍼의 필요성
##### CPU와 I/O 장치 간 속도 차이 해결
CPU의 데이터 처리 속도는 매우 빠르지만, I/O 장치의 속도는 상대적으로 느리다. CPU가 빠르게 데이터를 처리하는 동안, I/O 장치는 데이터를 빠르게 제공하지 못하므로 작업 지연이 발생할 수 있다. 버퍼는 이러한 속도 차이를 줄이기 위해 사용된다.

##### 대용량 데이터 처리의 효율성 향상
버퍼를 사용하면, 데이터를 **작은 단위로 여러 번 읽고 쓰는 대신** 한 번에 큰 단위로 읽고 쓸 수 있다. 이는 파일 입출력 및 네트워크 통신에서 데이터를 효과적으로 관리하는 데 필수적이다.

##### 데이터 전송의 안정성 제공
버퍼는 데이터 전송 과정에서 발생할 수 있는 일시적인 지연이나 손실을 방지하는 완충 역할을 하며, 안정적으로 데이터를 전송하고 받을 수 있게 돕는다.

------------------------------
#### 1-2 버퍼의 기본 구조와 원리
Java에서 제공하는 버퍼는 ```java.nio```패키지 내에 있는 추상 클래스 Buffer를 기반으로 설계되어 있으며, **데이터의 입출력 작업을 효과적으로** 관리할 수 있는 다양한 메커니즘을 제공한다. Buffer는 다음과 같은 기본 속성과 메소드를 통해 데이터의 읽기와 쓰기 과정을 관리한다.

-------------------------------
## 2. Buffer의 기본 속성
Java NIO의 버퍼는 다음의 세 가지 속성을 사용하여 데이터를 읽고 쓰는 작업을 효율적으로 관리한다.<br>
+ capacity : 버퍼의 총 크기를 나타내며, 버퍼가 최대한 저장할 수 있는 데이터의 양을 결정한다. ```capacity```는 생성 시 정해지며, 한 번 설정 되면 변경할 수 없다.<br>
+ position : 현재 데이터를 읽거나 쓰는 위치를 나타낸다. 데이터를 쓰거나 읽을 때마다 ```position```이 자동으로 증가하며, 데이터가 기록되거나 읽힌 마지막 위치를 추적한다.<br>
+ limit : 읽기나 쓰기 작업의 한계 위치를 나타낸다. 쓰기 모드일 때는 ```limit```가 ```capacity```와 같지만, 읽기 모드로 전환하면 ```limit```가 ```position``` 위치로 설정된다. ```limit```를 통해 버퍼의 작업 가능 범위를 제한할 수 있다. 

#### Buffer의 주요 메소드
+ flip() : 버퍼를 쓰기 모드에서 읽기 모드로 전환할 때 사용되며, ```position```을 0으로 설정하고, ```limit```를 현재 ```position```위치로 변경하여 읽기 작업의 범위를 설정한다.
+ clear() : 버퍼를 초기화하여 쓰기 작업을 위한 상태로 전환하며, ```position```을 0으로 설정하고, ```limit```를 ```capacity```로 변경한다. 기존 데이터는 지워지지 않고 재사용 가능 상태로 설정된다.
+ rewind() : ```position```을 0으로 설정하여 버퍼의 내용을 처음부터 읽을 수 있도록 한다. 쓰기 작업을 덮어쓰지 않고, 데이터를 반복해서 읽고자 할 때 유용하다.

##### 예제 : ByteBuffer의 기본 구조와 메소드 사용
```java
import java.nio.ByteBuffer;

public class BufferExample {
    public static void main(String[] args) {
        // 10 바이트 크기의 ByteBuffer 생성
        ByteBuffer buffer = ByteBuffer.allocate(10);

        // 데이터 쓰기
        for (int i = 0; i < buffer.capacity(); i++) {
            buffer.put((byte) (i + 1)); // 1, 2, 3, ..., 10 데이터 입력
        }

        // 버퍼의 쓰기 모드에서 읽기 모드로 전환
        buffer.flip();

        // 데이터 읽기
        while (buffer.hasRemaining()) {
            System.out.print(buffer.get() + " ");
        }

        // 버퍼 재사용을 위한 초기화
        buffer.clear();
    }
}
```
설명 : ```ByteBuffer``` 객체는 10 바이트의 크기로 생성되며, 1부터 10까지의 데이터를 입력한다.
데이터를 모두 입력한 후 ```flip()``` 메소드를 통해 쓰기 모드에서 읽기 모드로 전환하여 데이터의 ```position```을 0으로 설정하고, 읽기 범위를 ```limit```까지로 제한한다.
모든 데이터를 읽은 후 ```clear()```를 사용하여 버퍼를 초기화하여 재사용이 가능하게 한다.

----------------------------------------------
## 3. Buffer의 다양한 종류와 활용 목적
java NIO에서는 다양한 타입의 데이터를 저장하고 다루기 위한 여러 버퍼 클래스를 제공한다. 이를 통해 특정 데이터 타입에 최적화된 버퍼를 선택할 수 있다.

#### 3-1 ByteBuffer
ByteBuffer는 바이트(byte) 데이터를 저장하기 위한 버퍼로, 입출력 작업에서 가장 많이 사용된다. 파일 입출력이나 네트워크 통신에서 데이터를 바이트 단위로 저장하고 처리할 때 적합하다.
#### 3-2 CharBuffer
CharBuffer는 문자(char) 데이터를 저장하는 버퍼로, 문자열 데이터를 처리하는 데 유용하다. 특히 텍스트 파일 입출력에서 주로 사용되며,
```Chracter```데이터 타입을 저장할 수 있다.
#### 3-3 IntBuffer
IntBuffer는 정수(int)데이터를 저장하기 위한 버퍼로, 정수 배열을 입출력하거나 연산할 때 주로 사용된다. 대규모 정수 데이터를 저장하고 빠르게 읽고 쓸 수 있다.
#### 3-4 FloatBuffer, DoubleBuffer, LongBuffer, ShortBuffer
각각 부동소수(float), 배정밀도 부동소수(double), 긴 정수(long), 짧은 정수(short) 데이터를 저장할 수 있는 버퍼로, 대규모 과학 계산이나 데이터 분석 작업에서 효율적으로 데이터를 처리할 수 있다.

**각 버퍼 클래스는 allocate() 메소드를 통해 각 데이터 타입에 맞는 적절한 크기의 메모리 공간을 할당받을 수 있으며, 데이터의 읽기와 쓰기에 최적화되어 있다.**

-------------------------
## 4. Direct Buffer와 Non-Direct Buffer의 차이
Java NIO에서는 ```Direct Buffer와```와 ```Non-Direct Buffer``` 두 가지 방식의 버퍼를 제공하며, 메모리 할당 방식과 입출력 성능 면에서 차이가 있다.<br> 이 두 버퍼 방식은 각각의 목적에 맞게 활용할 수 있다.  

#### 4-1 Direct Buffer
Direct Buffer는 **네이티브 메모리(native memory)에** 할당되며, 입출력 장치와 직접 연결되어 데이터 전송 속도가 빠르다.
```ByteBuffer.allocateDirect()``` 메소드를 통해 생성되며, 다음과 같은 장점이 있다.
+ 고속 데이터 전송 : 네이티브 메모리에 직접 할당되므로 입출력 성능이 뛰어나며, 대규모 데이터 전송 시 유리하다.
+ 시스템 호출을 통한 메모리 접근 : JVM 힙 메모리 외부에 할당되어 네이티브 시스템 콜을 통해 메모리에 접근한다.
+ 일반적인 사용 : 파일 입출력, 네트워크 통신 등 대규모 데이터의 읽기 및 쓰기 작업에 사용된다.

#### 4-2 Non-Direct Buffer
Non-Direct Buffer는 **힙 메모리(heap memory)에** 할당되며, JVM 가비지 컬렉션의 대상이 된다. ```ByteBuffer.allocate()``` 메소드로 생성되며 다음과 같은 특성이 있다.
+ 빠른 메모리 할당 : 힙 메모리 내에서 버퍼가 생성되므로 메모리 할당 속도가 빠르고 JVM이 관리하기에 쉽다.
+ JVM 관리 하에 효율적 사용 : 힙 메모리에 할당되기 때문에 JVM이 직접 관리하고, 가비지 컬렉션으로 자동 해제되어 메모리 관리가 간편하다.
+ 일반적인 사용 : 상대적으로 소규모의 데이터

  |유형|메모리 위치|입출력 성능|장점|단점|
  |:---|:---|:---|:---|:---|
  |Direct Buffer|네이티브 메모리|빠름|대규모 데이터 전송에 유리, 빠른 입출력 가능|메모리 할당 및 해제 시간이 오래 걸림|
  |Non-Direct Buffer|힙 메모리|느림|메모리 할당이 빠르고 관리가 용이|입출력 성능이 떨어지며 가비지 컬렉션 대상|

#### 4-3 Direct Buffer의 활용 예제
```java
  import java.nio.ByteBuffer;

public class DirectBufferExample {
    public static void main(String[] args) {
        // Direct ByteBuffer 생성 (네이티브 메모리 할당)
        ByteBuffer directBuffer = ByteBuffer.allocateDirect(10);

        // 데이터 쓰기
        for (int i = 0; i < directBuffer.capacity(); i++) {
            directBuffer.put((byte) (i * 3));
        }

        // 버퍼 읽기 모드로 전환
        directBuffer.flip();

        // 데이터 읽기
        while (directBuffer.hasRemaining()) {
            System.out.print(directBuffer.get() + " ");
        }
    }
}
```
설명 : allocateDirect() 메소드를 통해 Direct Buffer를 생성하면, 네이티브 메모리에 버퍼가 할당된다. 네이트브 메모리에 직접 접근하기 때문에 입출력 작업에서 성능이 뛰어나다. ```put()```과 ```get()``` 메소드를 통해 데이터를 쓸 때마다 빠르게 읽기와 쓰기가 가능하다.

-----------------------------------
## 5. Buffer와 Channel을 이용한 입출력 처리
버퍼는 데이터를 임시 저장하는 메모리 영역이지만, **Channel**은 데이터를 읽고 쓰기 위한 입출력 경로이다. Buffer와 Channel을 결합하여 파일 입출력이나 네트워크 통신을 보다 빠르고 효율적으로 수행할 수 있다.
#### 5-1 FileChannel과 ByteBuffer를 이용한 파일 입출력
```FileChannel```은 파일을 읽거나 쓸 때 주로 사용되며, ByteBuffer와 함께 데이터 처리를 수행한다.

#### 5-2 FileChannel과 ByteChannel로 파일 읽고 쓰기
```java
import java.io.RandomAccessFile;
import java.nio.ByteBuffer;
import java.nio.channels.FileChannel;

public class FileChannelExample {
    public static void main(String[] args) throws Exception {
        // 파일을 열고 FileChannel 생성
        RandomAccessFile file = new RandomAccessFile("example.txt", "rw");
        FileChannel channel = file.getChannel();

        // ByteBuffer 생성 및 데이터 쓰기
        ByteBuffer buffer = ByteBuffer.allocate(64);
        buffer.put("Hello, Java NIO!".getBytes());

        // 쓰기 모드에서 읽기 모드로 전환 후 데이터 파일에 쓰기
        buffer.flip();
        channel.write(buffer);

        // 파일을 읽기 위해 채널의 위치를 처음으로 설정하고 버퍼 초기화
        channel.position(0);
        buffer.clear();

        // 파일에서 데이터 읽기
        channel.read(buffer);
        buffer.flip();

        // 읽은 데이터 출력
        while (buffer.hasRemaining()) {
            System.out.print((char) buffer.get());
        }

        // 채널과 파일 닫기
        channel.close();
        file.close();
    }
}

```
설명: ```FileChannel```과 ```ByteBuffer```를 이용해 파일에 데이터를 쓰고 다시 읽는 예제이다.
```flip()```으로 읽기 모드로 전환 후 ```write()```메소드를 통해 파일에 데이터를 쓴다.
```position```과 ```clear()```를 사용해 버퍼와 채널을 초기화 한 후, 데이터를 다시 읽어들이고 출력한다.
## 6. Buffer 실무 활용 사례
Java Buffer는 다양한 입출력 작업에서 효율성을 극대화하는데 사용된다. 실무에서는 주로 파일 입출력,네트워크 통신, 스트림 처리, 멀티미디어 재생 등에서 Buffer가 활용된다.

#### 6-1 파일 입출력(File I/O)
대용량 파일을 읽고 쓸 때 Buffer를 활용하여 **한 번에 일정한 크기의 데이터를 버퍼에 저장**하고 처리하면, 입출력 속도가 크게 향상된다. 예를 들어, 로그 파일을 주기적으로 읽거나 대용량 데이터를 파일에 저장하는 작업을 Buffer를 사용하면 효율적이다.

##### 예제 : 파일 입출력에서 Buffer 사용
```java
import java.io.RandomAccessFile;
import java.nio.ByteBuffer;
import java.nio.channels.FileChannel;

public class FileBufferExample {
    public static void main(String[] args) throws Exception {
        RandomAccessFile file = new RandomAccessFile("largefile.txt", "rw");
        FileChannel fileChannel = file.getChannel();
        ByteBuffer buffer = ByteBuffer.allocate(1024);  // 1KB 크기의 버퍼 생성

        // 파일에서 데이터 읽기
        while (fileChannel.read(buffer) > 0) {
            buffer.flip();  // 읽기 모드로 전환
            while (buffer.hasRemaining()) {
                System.out.print((char) buffer.get());
            }
            buffer.clear();  // 다음 읽기를 위해 버퍼 초기화
        }

        // 채널과 파일 닫기
        fileChannel.close();
        file.close();
    }
}
```
설명 : ```ByteBuffer```는 1KB의 크기로 생성되어 한 번에 많은 데이터를 읽고 쓸 수 있게 한다. ```FileChannel```을 사용하여 대용량 파일을 효율적으로 읽고 ```buffer.flip()```으로 읽기 모드로 전환하여 버퍼 내의 데이터를 출력한다. 파일 입출력에서 대용량 데이터를 처리할 때는 ByteBuffer와 FileChannel을 결합해 속도를 크게 높일 수 있다.

---------------------------
#### 6-2 네트워크 통신(Network Communication)
Buffer는 네트워크 소켓을 통한 데이터 송수신에서 특히 유용하다. 네트워크 데이터를 버퍼에 임시 저장하여 전송 속도를 최적화할 수 있으며, 연결 지연이 발생해도 버퍼 내 데이터가 손실되지 않는다.

##### 예제 : 네트워크 소켓에서 Buffer 사용
```java
import java.io.IOException;
import java.net.InetSocketAddress;
import java.nio.ByteBuffer;
import java.nio.channels.SocketChannel;

public class NetworkBufferExample {
    public static void main(String[] args) {
        try {
            // 서버에 연결할 소켓 채널 생성
            SocketChannel socketChannel = SocketChannel.open(new InetSocketAddress("localhost", 8080));

            // 송신 데이터 생성
            ByteBuffer buffer = ByteBuffer.allocate(1024);
            String message = "Hello, Server!";
            buffer.put(message.getBytes());

            // 읽기 모드로 전환 후 데이터 전송
            buffer.flip();
            socketChannel.write(buffer);

            // 응답 데이터 수신
            buffer.clear();
            socketChannel.read(buffer);
            buffer.flip();

            // 수신 데이터 출력
            while (buffer.hasRemaining()) {
                System.out.print((char) buffer.get());
            }

            // 채널 닫기
            socketChannel.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
설명 : ```SocketChannel```과 ```ByteBuffer```를 사용하여 서버와 통신한다.
클라이언트는 ```buffer.put()```으로 버퍼에 데이터를 쓰고, ```flip()```을 사용해 읽기 모드로 전환한 뒤 ```write()``` 메소드를 통해 서버로 데이터를 전송한다.
네트워크 통신에서는 데이터를 효율적으로 보내고 받을 수 있도록 Buffer가 중요한 역할을 한다.

#### 6-3 스트림 데이터 처리(Stream Processing)
스트림 데이터를 처리할 때 버퍼는 실시간으로 데이터를 유지하며 효율적으로 처리할 수 있다. 특히 비동기 스트림 처리가 필요한 대규모 데이터 처리 시스템에서 버퍼를 사용해 속도를 높인다.

##### 예제 : 파일 복사 작업에서 Buffer 사용
```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.nio.ByteBuffer;
import java.nio.channels.FileChannel;

public class FileCopyExample {
    public static void main(String[] args) throws Exception {
        // 입력 파일과 출력 파일 채널 생성
        FileInputStream fis = new FileInputStream("source.txt");
        FileOutputStream fos = new FileOutputStream("destination.txt");
        FileChannel inputChannel = fis.getChannel();
        FileChannel outputChannel = fos.getChannel();

        // 버퍼 생성
        ByteBuffer buffer = ByteBuffer.allocate(1024);

        // 파일 복사 작업
        while (inputChannel.read(buffer) > 0) {
            buffer.flip();
            outputChannel.write(buffer);
            buffer.clear();
        }

        // 채널과 스트림 닫기
        inputChannel.close();
        outputChannel.close();
        fis.close();
        fos.close();
    }
}
```
설명 : 파일 복사 작업에서 **Buffer**와 **FileChannel**을 활용하여 데이터를 한 번에 1KB씩 읽고 쓴다.
```clear```와 ```flip()```을 적절히 사용하여 버퍼를 초기화하고 읽기 모드로 전환하여 파일 복사를 수행한다.
이 방식은 기존의 파일 입출력 속도와 메모리 효율성이 뛰어나며, 스트림 데이터 처리에서도 효율적인 입출력을 가능하게 한다.

------------------------------------
## 7. Buffer와 Channel의 구체적인 활용 방식
자바 NIO에서 Buffer와 Channel은 입출력 작업의 성능을 최적화 하기 위해 함께 사용된다. Buffer는 데이터를 저장하고, Channel은 데이터의 통로 역할을 하며, 데이터가 Channel을 통해 Buffer로 이동하면서 읽기와 쓰기 작업이 이루어진다.

#### 7-1 FileChannel과 ByteBuffer의 협력 구조
+ 데이터 쓰기 : ```ByteBuffer```에 데이터를 쓰고 ```flip()```메소드로 읽기 모드로 전환한다. 이후 ```FileChannel.write() 메소드를 사용해 버퍼에 있는 데이터를 파일로 전송한다.
+ 데이터 읽기 : ```FileChannel.read()``` 메소드를 사용해 파일 데이터를 ```ByteBuffer```로 읽어온다. 버퍼의 데이터를 읽기 위해 ```filp()```을 호출하여 읽기 모드로 전환하고, ```get()``` 메소드를 사용해 버퍼에 저장된 데이터를 읽는다.

##### 예제 : FileChannel과 ByteBuffer를 활용한 파일 읽기
```java
import java.io.RandomAccessFile;
import java.nio.ByteBuffer;
import java.nio.channels.FileChannel;

public class FileReadExample {
    public static void main(String[] args) throws Exception {
        RandomAccessFile file = new RandomAccessFile("data.txt", "r");
        FileChannel channel = file.getChannel();
        ByteBuffer buffer = ByteBuffer.allocate(1024);

        int bytesRead = channel.read(buffer);
        while (bytesRead != -1) {
            buffer.flip();
            while (buffer.hasRemaining()) {
                System.out.print((char) buffer.get());
            }
            buffer.clear();
            bytesRead = channel.read(buffer);
        }

        channel.close();
        file.close();
    }
}
```
설명 : ```FileChannel```은 데이터를 ```ByteBuffer```에 읽어 들이며, ```flip()```을 통해 읽기 모드로 전환한 후 버퍼의 내용을 출력한다. 데이터를 모두 읽으면 ```clear()```를 통해 버퍼를 초기화하여 다음 읽기 작업을 준비한다. Buffer와 Channel의 조합은 대용량 데이터를 효과적으로 처리하는 데 유용하다.

--------------------------
## 8. Buffer 관련 주요 개념 요약
|개념|설명|
|:---|:---|
|Buffer|데이터를 임시로 저장하여 CPU와 I/O의 장치 간의 속도 차이를 보완하고, 입출력 성능을 높인다.|
|Capacity|버퍼의 총 용량으로, 저장할 수 있는 데이터의 최대량을 나타낸다.|
|Position|버퍼의 현재 위치로, 읽기나 쓰기를 수행할 위치를 나타낸다.|
|Limit|읽기나 쓰기의 한계 위치로, 읽기/쓰기 가능한 범위를 지정한다.|
|Filp()|쓰기 모드에서 읽기 모드로 전환하여 읽기 가능한 상태로 설정한다.|
|Clear()|버퍼를 초기화하여 다시 데이터를 쓸 수 있도록 준비한다.
|Rewind()|Position을 0으로 설정하여 처음부터 데이터를 읽을 수 있도록 한다.|
|Direct Buffer|네이티브 메모리에 할당되며, 대용량 데이터 입출력에 유리하다.|
|Non-Direct Buffer|힙 메모리에 할당되며, 일반적인 데이터 입출력에 적합하다.|
