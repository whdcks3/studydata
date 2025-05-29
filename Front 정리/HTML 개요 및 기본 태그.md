# 1. 웹의 동작 원리
## 1-1. HTML, CSS, JavaScript의 역할
웹 페이지는 단순한 정적인 문서가 아니라, 사용자와 상호작용할 수 있도록 다양한 기술이 결합된 구조로 이루어져 있다. 그 중심에는 HTML, CSS, JavaScript가 있으며, 각각의 역할이 다르지만 서로 긴밀하게 협력하여 웹 페이지를 완성한다.

### HTML: 문서의 구조를 정의하는 언어
HTML(HyperText Markup Language)은 **웹 페이지의 기본 구조를 정의하는 마크업 언어**이다.<br>
HTML 문서를 통해 텍스트, 이미지, 비디오, 링크 등의 요소를 배치할 수 있으며, 웹 브라우저는 이 HTML 코드를 해석하여 사용자에게 내용을 표시한다.

웹 페이지를 하나의 게임 캐릭터에 비유해보자. 게임 속 캐릭터는 **몸의 형태(골격)** 가 있어야 하며, 여기에 **스킨(디자인)**과 **움직임(기능)** 이 추가된다.<br>
이때 HTML은 캐릭터의 뼈대를 만드는 역할을 한다. 즉, 아무런 디자인이나 동적인 기능이 없는 순수한 구조만을 정의한다.

**HTML의 주요 특징**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;웹 문서의 구조를 정의: 제목, 본문, 이미지, 리스트, 표 등의 요소를 배치한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;태그를 이용하여 문서의 의미를 표현: ```<h1>, <p>, <a>, <table>``` 등의 태그를 사용하여 정보를 구성한다. <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CSS 및 JavaScript와 결합하여 스타일 및 동적 기능을 추가할 수 있도록 지원한다.

**HTML의 기본 예제**
아래 HTML 코드는 간단한 웹 페이지의 기본적인 구조를 정의한다.

```HTML
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>HTML의 역할</title>
  </head>
  <body>
    <h1>HTML은 웹 페이지의 구조를 정의하는 언어</h1>
    <p>
      HTML은 웹 문서의 제목, 본문, 이미지, 링크 등의 요소를 배치하는 역할을
      한다.
    </p>
  </body>
</html>
```

위의 코드에서:

```<!DOCTYPE html>```: 문서가 HTML5 형식임을 선언한다.<br>
```<html>```: HTML 문서의 최상위 요소이다.<br>
```<head>```: 문서의 메타데이터와 스타일, 스크립트를 포함한다.<br>
```<body>```: 실제 웹 페이지에 표시될 내용을 담고 있다.

이처럼 HTML은 웹 페이지에서 콘텐츠의 구조를 정의하는 역할을 한다.

-----------------
### CSS: 스타일과 디자인을 적용하는 언어
CSS(Cascading Style Sheets)는 HTML 문서의 디자인을 설정하는 스타일링 언어이다.
HTML이 웹 페이지의 골격이라면, CSS는 색상, 레이아웃, 글꼴, 배경 이미지 등을 조정하여 페이지를 미적으로 꾸미는 역할을 한다.

게임 캐릭터의 예시로 다시 설명하자면, HTML이 캐릭터의 몸의 형태라면, CSS는 캐릭터가 입는 옷, 장신구, 무기, 스킨 등을 결정하는 요소이다.

### CSS의 주요 특징
HTML 요소의 스타일을 변경: 색상, 크기, 배경, 테두리 등을 설정할 수 있다.<br>
웹 페이지의 레이아웃을 구성: flexbox, grid 등을 사용하여 화면 배치를 조정할 수 있다.<br>
반응형 웹 디자인을 지원: 다양한 화면 크기에 맞게 스타일을 변경할 수 있다.
CSS의 기본 적용 방법
CSS는 HTML에 여러 방식으로 적용할 수 있다.

인라인 스타일(Inline CSS)
개별 요소에 직접 style 속성을 이용하여 적용하는 방식이다.

<p style="color: blue; font-size: 18px;">
  CSS는 웹 페이지의 스타일을 변경할 수 있다.
</p>
내부 스타일(SInternal CSS)
HTML 문서 내 <style> 태그를 사용하여 스타일을 정의하는 방식이다.

<style>
  p {
    color: red;
    font-size: 16px;
  }
</style>
외부 스타일(External CSS) 별도의 .css 파일을 만들어 HTML에서 불러오는 방식이다.

<link rel="stylesheet" href="styles.css" />
CSS를 사용하면 웹 페이지의 일관된 디자인을 유지하고, 유지보수도 쉽게 할 수 있다.

JavaScript: 웹 페이지에 동적 기능을 추가하는 언어
JavaScript는 웹 페이지를 동적으로 만들고 사용자와 상호작용할 수 있도록 하는 프로그래밍 언어이다.
HTML이 페이지의 구조를 담당하고, CSS가 디자인을 담당한다면, JavaScript는 사용자의 행동(클릭, 입력 등)에 반응하여 페이지를 동적으로 변경할 수 있도록 돕는다.

게임 개발에서 캐릭터의 움직임, 공격, 점프 등의 동작을 구현하는 것이 JavaScript의 역할과 비슷하다.
즉, 웹 페이지에서도 JavaScript를 활용하여 버튼을 클릭하면 내용이 바뀌거나, 애니메이션이 실행되거나, 데이터를 서버에서 받아오는 등의 다양한 기능을 추가할 수 있다.

JavaScript의 주요 특징
사용자 이벤트를 처리: 버튼 클릭, 키보드 입력, 마우스 움직임 등의 이벤트를 감지하여 동작을 수행한다.
HTML 요소를 동적으로 변경: document.getElementById() 등의 메서드를 이용하여 HTML 요소를 조작할 수 있다.
애니메이션과 효과를 추가: CSS와 함께 사용하여 화면 전환, 슬라이드 효과 등을 구현할 수 있다.
서버와 비동기 통신(AJAX, Fetch API) : 백엔드 서버에서 데이터를 가져와 웹 페이지를 업데이트할 수 있다.
JavaScript의 기본 예제
아래 예제는 버튼을 클릭하면 문장의 내용을 변경하는 간단한 JavaScript 코드이다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>JavaScript 예제</title>
  </head>
  <body>
    <h1>JavaScript로 동적인 기능 추가</h1>
    <p id="text">버튼을 클릭하면 이 문장이 변경됩니다.</p>
    <button onclick="changeText()">클릭</button>

    <script>
      function changeText() {
        document.getElementById("text").innerText =
          "JavaScript가 동작하여 텍스트가 변경되었습니다!";
      }
    </script>
  </body>
</html>
위 코드에서:

document.getElementById("text").innerText를 사용하여 <p> 태그의 내용을 변경할 수 있다.
onclick="changeText()"를 버튼에 추가하여 클릭 시 함수가 실행되도록 했다.
이처럼 JavaScript를 활용하면 웹 페이지를 동적으로 조작하고, 사용자의 입력에 반응할 수 있다.

HTML, CSS, JavaScript의 협업
웹 페이지가 제대로 동작하려면 HTML, CSS, JavaScript가 서로 협력해야 한다.

HTML이 콘텐츠의 구조를 담당하고,
CSS가 디자인을 적용하며,
JavaScript가 동적인 기능을 추가한다.
이 세 가지 요소가 조화롭게 사용될 때, 비로소 사용자가 원하는 기능을 갖춘 웹 페이지가 완성된다.

학습자의 사고를 돕기 위한 질문
HTML, CSS, JavaScript가 각각 담당하는 역할은 무엇인가?

웹 페이지에서 각 요소가 어떤 기능을 수행하는지 생각해보라.
HTML 문서에서 CSS와 JavaScript를 분리하여 작성하는 것이 유지보수에 왜 유리한가?

코드의 재사용성과 유지보수성을 고려해보라.
1.2. 브라우저의 렌더링 과정
웹 브라우저는 HTML 문서를 해석하여 사용자가 볼 수 있는 화면을 렌더링한다.
렌더링 과정은 단순히 HTML 파일을 읽어서 화면에 출력하는 것이 아니라, 여러 단계를 거쳐 최종적으로 웹 페이지를 표시하는 복잡한 절차이다.
이 과정을 이해하면 웹 페이지가 어떻게 동작하는지 파악할 수 있으며, 렌더링 최적화를 통해 성능을 개선할 수도 있다.

웹 브라우저가 HTML 문서를 화면에 표시하는 과정은 다음과 같이 진행된다.

HTML 문서 요청 및 응답
DOM(Document Object Model) 트리 생성
CSSOM(CSS Object Model) 트리 생성 및 적용
렌더 트리(Render Tree) 생성
레이아웃(Layout) 계산
페인팅(Painting) 및 화면에 표시
이제 각 단계별로 자세히 살펴보자.

HTML 문서 요청 및 응답
웹 브라우저는 사용자가 웹 페이지를 요청하면 HTTP 요청을 보내고, 서버로부터 해당 HTML 파일을 받아온다.
이 과정은 클라이언트-서버 모델을 기반으로 동작하며, 브라우저는 사용자가 입력한 URL을 바탕으로 DNS 서버에서 IP 주소를 조회한 후 요청을 보낸다.

예를 들어, 사용자가 https://example.com을 입력하면:

브라우저는 DNS 서버에서 example.com의 IP 주소를 조회한다.
해당 IP 주소를 가진 서버로 HTTP 요청(GET 요청) 을 보낸다.
서버는 요청을 처리한 후 HTML 파일을 응답(Response) 으로 반환한다.
이때 서버가 반환하는 응답은 HTML뿐만 아니라, CSS, JavaScript, 이미지 등 웹 페이지를 구성하는 모든 자원을 포함할 수 있다.

DOM(Document Object Model) 트리 생성
웹 브라우저가 HTML 파일을 받으면 이를 해석하여 DOM(Document Object Model) 트리를 생성한다.
DOM은 웹 페이지의 계층적 구조를 나타내는 객체 모델로, 각 HTML 요소를 노드(Node)로 변환하여 트리 형태로 구성된다.

예를 들어, 다음과 같은 HTML이 있다고 가정하자.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <title>렌더링 과정</title>
  </head>
  <body>
    <h1>브라우저의 렌더링 과정</h1>
    <p>이 페이지는 렌더링 과정의 이해를 돕기 위한 예제입니다.</p>
  </body>
</html>
이 HTML 문서를 브라우저가 해석하면, 다음과 같은 DOM 트리가 생성된다.

Document
 ├── html
 │   ├── head
 │   │   └── title
 │   ├── body
 │   │   ├── h1
 │   │   ├── p
각 HTML 요소(<html>, <head>, <body> 등)가 트리 구조의 노드(Node) 로 변환되며, 이 DOM은 이후 JavaScript에서 조작할 수 있다.

DOM 트리는 브라우저가 HTML을 해석하는 즉시 생성되며, 이후 CSS와 JavaScript가 적용될 준비를 한다.

CSSOM(CSS Object Model) 트리 생성 및 적용
HTML이 DOM 트리로 변환되었다면, 이제 CSS를 처리할 차례다.
웹 페이지가 CSS를 포함하고 있다면 브라우저는 CSS 파서(Parser) 를 이용해 CSS 스타일을 분석하고, 이를 기반으로 CSSOM(CSS Object Model) 트리를 생성한다.

예를 들어, 다음과 같은 CSS 코드가 있다고 가정하자.

h1 {
  color: blue;
  font-size: 24px;
}
p {
  color: gray;
}
이 CSS는 다음과 같은 CSSOM 트리로 변환된다.

CSSOM
 ├── h1
 │   ├── color: blue
 │   ├── font-size: 24px
 ├── p
     ├── color: gray
브라우저는 이 CSSOM을 이용하여 각 HTML 요소에 스타일을 적용할 준비를 한다.

DOM과 CSSOM의 차이점

DOM: HTML 요소의 구조와 관계를 나타내는 트리
CSSOM: 각 요소에 적용되는 스타일 정보를 나타내는 트리
렌더 트리(Render Tree) 생성
브라우저는 HTML의 DOM 트리와 CSS의 CSSOM 트리를 결합하여 렌더 트리(Render Tree) 를 생성한다.
렌더 트리는 실제로 화면에 표시할 요소만 포함하는 트리이다.

예를 들어, <head> 내부의 <title> 요소나 display: none;이 적용된 요소는 렌더 트리에 포함되지 않는다.

<body>
  <h1>렌더링 과정</h1>
  <p style="display: none;">이 문장은 보이지 않습니다.</p>
</body>
이 HTML과 CSS를 조합하면, 최종적인 렌더 트리는 다음과 같이 구성된다.

Render Tree
 ├── h1 (color: blue, font-size: 24px)
렌더 트리의 특징

화면에 표시할 요소만 포함한다.
각 요소가 CSS 스타일을 포함한 상태로 존재한다.
이제 브라우저는 렌더 트리를 기반으로 화면 배치를 계산하는 단계로 넘어간다.

레이아웃(Layout) 계산
렌더 트리가 생성되었다면, 이제 각 요소의 위치와 크기를 계산하는 과정이 필요하다.
이 과정을 레이아웃(Layout) 계산이라고 하며, 브라우저는 화면 크기에 따라 각 요소를 배치한다.

예를 들어, <h1> 태그가 가로 너비 100% 를 차지한다고 가정해보자.

h1 {
  width: 100%;
  margin: 10px;
}
브라우저는 해당 요소의 너비, 높이, 좌표 위치 등을 계산하여 화면에서 어디에 배치할지를 결정한다.

레이아웃 과정에서는 다음과 같은 요소들이 고려된다.

각 요소의 크기(width, height)
요소 간의 간격(margin, padding)
컨테이너 안에서의 위치(position, flexbox, grid 등)
페인팅(Painting) 및 화면에 표시
마지막 단계는 실제 화면에 픽셀을 그리는 과정, 즉 페인팅(Painting) 이다.
브라우저는 이전 단계에서 계산한 레이아웃 정보를 GPU(Graphics Processing Unit) 를 사용하여 화면에 렌더링한다.

이 과정에서 브라우저는 다음을 수행한다.

색상과 스타일을 적용하여 요소를 화면에 출력한다.
텍스트를 화면에 그린다.
그림자, 테두리, 배경 이미지 등의 스타일을 적용한다.
페인팅이 완료되면, 최종적으로 사용자가 웹 페이지를 볼 수 있는 상태가 된다.

렌더링 과정의 흐름 정리
HTML을 요청하고 응답을 받는다.
HTML을 해석하여 DOM 트리를 생성한다.
CSS를 해석하여 CSSOM 트리를 생성한다.
DOM과 CSSOM을 결합하여 렌더 트리를 만든다.
각 요소의 위치와 크기를 계산하는 레이아웃 과정을 거친다.
페인팅 단계에서 화면에 실제 픽셀을 그린다.
이 과정을 통해 브라우저는 HTML을 시각적으로 변환하고, 사용자가 볼 수 있는 웹 페이지를 생성한다.

학습자의 사고를 돕기 위한 질문
웹 브라우저가 HTML, CSS, JavaScript 파일을 처리하는 과정은 어떻게 되는가?

DOM, CSSOM, 렌더링 엔진의 역할을 떠올려보라.
브라우저에서 JavaScript 실행이 CSS 렌더링에 영향을 줄 수 있는 이유는 무엇인가?

JavaScript의 동기/비동기 실행과 CSS 적용 과정을 생각해보라.
1.3. 클라이언트-서버 모델
웹은 기본적으로 클라이언트(Client)와 서버(Server) 간의 통신을 기반으로 작동한다.
클라이언트는 웹 브라우저이며, 사용자가 웹 사이트에 접속할 때 서버에 요청(Request)을 보내고, 서버는 이에 대한 응답(Response)을 클라이언트에게 반환하는 구조로 동작한다.

이러한 방식은 클라이언트-서버 모델(Client-Server Model) 이라 불리며, 웹뿐만 아니라 다양한 네트워크 기반 애플리케이션에서도 사용된다.

클라이언트와 서버의 역할
클라이언트(Client)

사용자가 직접 조작하는 장치(PC, 스마트폰, 태블릿 등)에서 실행되는 웹 브라우저(Chrome, Firefox, Edge 등).
사용자가 입력한 URL을 기반으로 웹 페이지 요청을 서버에 전송한다.
서버로부터 받은 HTML, CSS, JavaScript 파일을 해석하여 화면에 표시한다.
JavaScript를 실행하여 동적 기능을 처리하고, 필요할 경우 서버와 추가적인 데이터 통신을 한다.
서버(Server)

클라이언트의 요청을 처리하고, 적절한 데이터를 응답하는 역할을 수행하는 컴퓨터 시스템.
보통 웹 서버(Web Server) 와 데이터베이스 서버(Database Server) 로 나뉘며, 각기 다른 역할을 수행한다.
요청된 HTML, CSS, JavaScript 파일을 반환하거나, 클라이언트에서 전송한 데이터를 데이터베이스에 저장하고 다시 응답할 수도 있다.
클라이언트-서버 모델의 동작 과정
웹 사이트를 요청하는 과정은 다음과 같은 단계를 거친다.

사용자가 웹 페이지 요청

사용자가 브라우저에 https://example.com을 입력한다.
브라우저는 DNS 서버를 통해 해당 도메인의 IP 주소를 조회한다.
조회된 IP 주소를 기반으로 웹 서버에 HTTP 요청을 보낸다.
서버에서 요청 처리

웹 서버는 클라이언트의 요청을 확인하고, 요청한 리소스(HTML, CSS, JavaScript 등)를 찾아서 반환한다.
요청한 리소스가 동적 데이터라면, 서버 내부에서 백엔드 프로세스(예: PHP, Node.js, Java Spring 등)를 통해 데이터베이스와 통신한 후 데이터를 생성한다.
클라이언트로 응답 반환

서버는 HTTP 응답을 통해 클라이언트에게 HTML, CSS, JavaScript 등의 데이터를 전송한다.
브라우저는 받은 HTML을 파싱하여 화면을 렌더링한다.
추가적인 요청 처리 (AJAX, API 요청 등)

웹 페이지가 로드된 후, JavaScript는 필요할 경우 추가적인 데이터를 요청할 수 있다.
예를 들어, 사용자가 검색 버튼을 클릭하면, 브라우저는 추가적인 API 요청을 서버에 보낸다.
서버는 해당 요청을 처리한 후 JSON 형태의 응답을 반환할 수 있다.
HTTP 프로토콜과 요청/응답 구조
웹에서 클라이언트와 서버 간 통신은 HTTP(HyperText Transfer Protocol) 를 통해 이루어진다.
HTTP는 요청(Request)과 응답(Response) 기반의 프로토콜이며, 클라이언트가 서버에 요청을 보내면, 서버는 이에 대한 응답을 반환하는 구조로 동작한다.

HTTP 요청(Request)

클라이언트가 서버에 요청을 보낼 때 사용되는 메시지.
요청 방식(Method)에는 GET, POST, PUT, DELETE 등이 있다.
예를 들어, 웹 브라우저에서 웹 페이지를 요청하면 GET 요청이 전송된다.
요청 메시지의 예시:

GET /index.html HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Accept: text/html,application/xhtml+xml
HTTP 응답(Response)

서버가 요청을 처리한 후 클라이언트에게 반환하는 메시지.
응답에는 상태 코드(Status Code)와 함께 HTML, JSON 등의 데이터가 포함될 수 있다.
응답 메시지의 예시:

HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 5123

<html>
    <head>
        <title>Example Page</title>
    </head>
    <body>
        <h1>안녕하세요, 웹 페이지입니다!</h1>
    </body>
</html>
여기서 200 OK는 요청이 정상적으로 처리되었음을 의미하는 상태 코드이다.

클라이언트-서버 모델을 활용한 게임 개발 예제
게임 개발에서도 클라이언트-서버 모델이 중요하게 사용된다.
예를 들어, 멀티플레이어 온라인 게임을 만들 때 클라이언트(게임 앱)와 서버(게임 데이터 처리 및 매칭 시스템) 간의 통신이 필수적이다.

예제: 게임 클라이언트가 서버에 플레이어 정보를 요청하는 경우

게임 클라이언트는 GET /player/1234 요청을 서버에 보낸다.
서버는 해당 ID(1234)를 가진 플레이어 데이터를 데이터베이스에서 조회한 후 JSON으로 응답한다.
{
  "playerId": 1234,
  "nickname": "WarriorX",
  "level": 15,
  "score": 15000
}
게임 클라이언트는 이 JSON 데이터를 받아 화면에 표시하거나, 게임 내 로직에 반영할 수 있다.
클라이언트-서버 모델의 장점과 단점
장점

데이터 중앙화

모든 데이터를 서버에서 관리하므로 보안과 백업이 용이하다.
다양한 클라이언트 지원

웹 브라우저뿐만 아니라 모바일 앱, 게임 클라이언트 등 다양한 환경에서 동일한 서버와 통신할 수 있다.
확장성(Scalability)

서버의 성능을 향상시키거나, 여러 개의 서버를 운영하여 많은 클라이언트 요청을 처리할 수 있다.
단점

서버 부하 문제

많은 요청이 몰리면 서버의 성능이 저하될 수 있다.
이를 해결하기 위해 로드 밸런싱(Load Balancing)과 캐싱(Caching) 기법이 필요하다.
인터넷 의존성

클라이언트가 서버와 통신해야 하기 때문에 네트워크 연결이 필요하다.
오프라인 상태에서는 기능이 제한될 수 있다.
학습자의 사고를 돕기 위한 질문
클라이언트와 서버가 데이터를 주고받는 과정에서 HTTP 요청과 응답의 역할은 무엇인가?

클라이언트가 요청을 보내고 서버가 응답하는 과정을 단계별로 생각해보라.
웹에서 클라이언트가 서버로 요청을 보낼 때, GET과 POST 요청의 차이는 무엇인가?

데이터를 전달하는 방식과 보안적인 차이를 고려해보라.
2. HTML 문서 구조
2.1. HTML 문서의 기본 구조
HTML 문서는 웹 페이지의 뼈대(Skeleton) 역할을 한다.
모든 HTML 문서는 특정한 구조를 따르며, 이를 통해 브라우저가 올바르게 웹 페이지를 해석하고 렌더링할 수 있다.

HTML 문서의 기본 구조는 다음과 같이 구성된다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>HTML 문서 구조</title>
  </head>
  <body>
    <h1>HTML 문서 구조</h1>
    <p>이것은 HTML 문서의 기본 구조입니다.</p>
  </body>
</html>
위 코드를 구성하는 각 요소에 대해 자세히 살펴보자.

DOCTYPE 선언 (<!DOCTYPE html>)
HTML 문서의 맨 처음에는 <!DOCTYPE html> 선언이 포함된다.
이 선언은 문서가 HTML5 표준을 따르고 있음을 브라우저에게 알리는 역할을 한다.

HTML5에서는 <!DOCTYPE html>만 선언하면 되지만, 과거 HTML4나 XHTML에서는 복잡한 DOCTYPE 선언이 필요했다.
올바르게 선언하지 않으면 브라우저가 Quirks Mode(비표준 모드) 로 렌더링할 수 있으며, 예상과 다른 결과가 발생할 수 있다.
예를 들어, HTML4의 DOCTYPE 선언은 다음과 같이 복잡했다.

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
HTML5에서는 간단히 <!DOCTYPE html>만 작성하면 된다.

HTML 문서의 루트 요소 (<html> 태그)
HTML 문서는 <html> 태그로 감싸져 있다.
이 태그는 문서의 루트(root) 요소이며, 모든 HTML 요소는 이 안에 포함된다.

<html> 태그에는 보통 lang 속성이 포함된다.
lang="ko"를 설정하면 문서의 기본 언어가 한국어임을 의미한다.
이 설정은 검색 엔진(SEO)과 스크린 리더(Screen Reader)와 같은 보조 기술에 영향을 준다.
예제:

<html lang="ko">
  ...
</html>
메타데이터를 포함하는 <head> 태그
<head> 태그는 문서의 메타데이터(Metadata)를 포함하며,
웹 페이지가 어떻게 표시될지를 정의하는 요소들을 포함한다.

다음은 <head> 태그 내부의 주요 요소들이다.

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>웹 페이지 제목</title>
</head>
<meta charset="UTF-8">

HTML 문서에서 사용할 문자 인코딩을 지정한다.
UTF-8을 설정하면 한글, 일본어, 중국어 등 다국어 문자 표시가 가능하다.
<meta name="viewport" content="width=device-width, initial-scale=1.0">

반응형 웹을 위해 설정하는 메타 태그.
width=device-width는 화면의 너비를 기기(device)의 너비와 동일하게 맞춘다.
initial-scale=1.0은 페이지의 기본 확대/축소 비율을 설정한다.
<title>

브라우저 탭과 검색 결과에서 표시될 웹 페이지의 제목을 설정한다.
예제:

<title>게임 개발 블로그</title>
위와 같이 설정하면, 웹 브라우저의 탭에는 "게임 개발 블로그" 라는 제목이 표시된다.

웹 페이지의 콘텐츠를 포함하는 <body> 태그
<body> 태그는 HTML 문서에서 실제로 화면에 표시될 내용을 포함한다.
즉, 사용자가 볼 수 있는 텍스트, 이미지, 버튼 등의 요소가 들어간다.

예제:

<body>
  <h1>게임 개발 기본 지식</h1>
  <p>이 페이지에서는 HTML 문서의 기본 구조를 설명합니다.</p>
</body>
위 코드에서 <h1> 태그는 페이지의 제목을 나타내고, <p> 태그는 단락을 나타낸다.

HTML 문서의 전체적인 구조 정리
HTML 문서는 <!DOCTYPE> → <html> → <head> → <body> 순으로 구성된다.
각 부분이 하는 역할을 다시 정리하면 다음과 같다.

<!DOCTYPE html> → HTML5 문서임을 선언
<html> → 문서의 루트 요소
<head> → 메타데이터 포함 (문서 정보, 스타일, 외부 파일 연결)
<body> → 화면에 표시되는 콘텐츠 포함
이러한 구조를 이해하면 HTML 문서를 올바르게 작성할 수 있으며,
게임 개발에서도 웹 기반 게임을 만들거나 게임의 공식 웹사이트를 제작할 때 유용하게 활용할 수 있다.

학습자의 사고를 돕기 위한 질문
HTML 문서에서 <head>와 <body> 태그의 역할은 각각 무엇인가?

웹 페이지에서 보이는 요소와 보이지 않는 요소의 차이를 생각해보라.
웹 브라우저가 HTML 문서를 해석할 때 <!DOCTYPE html> 선언이 필요한 이유는 무엇인가?

문서의 렌더링 모드를 결정하는 방식에 대해 생각해보라.
실습 문제
문제 1: HTML 문서의 기본 구조 작성하기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<!DOCTYPE html>을 선언한다.
<html>, <head>, <body> 태그를 포함한다.
<title> 태그를 사용하여 페이지 제목을 "내 첫 번째 웹 페이지"로 설정한다.
2.2. <head> 태그의 구성 요소
웹 문서에서 <head> 태그는 메타데이터(metadata) 를 포함하는 영역이다.
메타데이터는 브라우저와 검색 엔진, 그리고 다양한 시스템이 웹 페이지를 어떻게 해석하고 표시해야 하는지를 정의하는 정보를 담는다.

이 <head> 태그에는 다양한 요소들이 포함되며, 대표적인 요소들은 다음과 같다.

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta
    name="description"
    content="이 웹사이트는 게임 개발 관련 정보를 제공합니다."
  />
  <meta name="keywords" content="게임 개발, HTML, CSS, JavaScript" />
  <meta name="author" content="홍길동" />
  <title>게임 개발 블로그</title>
  <link rel="stylesheet" href="styles.css" />
  <script src="script.js" defer></script>
</head>
위 코드를 구성하는 각각의 요소를 자세히 살펴보자.

1. <title> 태그: 웹 페이지 제목 설정
<title> 태그는 웹 페이지의 제목(Title)을 지정하는 역할을 한다.
브라우저 탭에 표시되는 제목이며, 검색 엔진(SEO)에서도 중요한 역할을 한다.

<title>게임 개발 블로그</title>
이 코드를 포함하면, 사용자가 해당 웹 페이지를 방문했을 때 브라우저의 탭(Tabs) 에 게임 개발 블로그라는 제목이 표시된다.

또한 검색 엔진에서 웹 페이지를 찾을 때, 검색 결과의 제목으로도 사용된다.

예를 들어, 검색 엔진 결과 화면에서 이렇게 보일 수 있다.

게임 개발 블로그 - HTML 기초 배우기
https://example.com/game-dev
이 블로그에서는 HTML, CSS, JavaScript를 활용한 게임 개발 기초를 배울 수 있습니다.
2. <meta charset="UTF-8">: 문자 인코딩 설정
<meta charset="UTF-8"> 태그는 문서의 문자 인코딩 방식을 정의한다.

<meta charset="UTF-8" />
UTF-8은 한글, 영어, 일본어, 중국어 등 대부분의 언어를 지원하는 대표적인 문자 인코딩 방식이다.

이 설정이 없으면, 브라우저가 문자를 잘못 해석하여 한글이 깨지는 문제(문자 인코딩 오류) 가 발생할 수 있다.

3. <meta name="viewport">: 반응형 웹을 위한 설정
웹 페이지를 모바일 친화적으로 만들기 위해 사용하는 메타 태그이다.

<meta name="viewport" content="width=device-width, initial-scale=1.0" />
width=device-width → 페이지의 너비를 기기 화면의 너비와 동일하게 설정.
initial-scale=1.0 → 기본 확대/축소 비율을 100%로 설정.
이 설정이 없으면 모바일 화면에서 웹 페이지가 지나치게 작게 표시될 수 있다.

예를 들어, 이 태그 없이 웹 사이트를 열면 다음과 같은 문제가 발생할 수 있다.

[잘못된 예시]

데스크톱 화면을 기준으로 레이아웃이 고정되어, 스마트폰에서는 글자가 너무 작게 보임.
사용자가 손가락으로 확대해야만 읽을 수 있음.
[올바른 예시]

기기의 화면 크기에 맞춰서 웹 페이지가 자동 조정됨.
스마트폰에서도 가독성이 좋고 조작이 쉬움.
4. <meta name="description">: 웹 페이지 설명
이 태그는 검색 엔진(SEO)에 중요한 영향을 미친다.
웹 페이지의 설명을 지정하여 검색 결과에 표시되는 내용을 결정한다.

<meta
  name="description"
  content="이 웹사이트는 게임 개발 관련 정보를 제공합니다."
/>
검색 결과에서 웹 페이지를 찾을 때, 이 설명이 표시될 수 있다.

예를 들어, 위 태그가 포함된 웹 페이지가 검색 결과에 나오면 다음과 같이 보일 수 있다.

게임 개발 블로그 - HTML 기초 배우기
https://example.com/game-dev
이 웹사이트는 게임 개발 관련 정보를 제공합니다.
즉, 이 태그는 사용자가 웹 페이지를 클릭할지 말지를 결정하는 중요한 역할을 한다.

5. <meta name="keywords">: 키워드 설정 (최근에는 중요도가 낮아짐)
이 태그는 웹 페이지에서 다루는 핵심 키워드(검색어)를 명시하는 역할을 한다.

<meta name="keywords" content="게임 개발, HTML, CSS, JavaScript" />
과거에는 검색 엔진이 이 정보를 활용하여 웹 페이지를 분류했지만,
최근에는 검색 엔진 알고리즘이 발전하여 이 태그의 중요도가 크게 낮아졌다.
하지만 여전히 사용되는 경우가 있으므로 알아두면 좋다.

6. <meta name="author">: 문서 작성자 정보
이 태그는 웹 페이지의 저자(author) 를 나타낸다.

<meta name="author" content="홍길동" />
이렇게 설정하면, 해당 웹 페이지를 만든 사람이 홍길동임을 나타낼 수 있다.

특정 기업이나 팀이 웹사이트를 관리하는 경우, 이 정보는 문서의 저작권 관리에도 활용될 수 있다.

7. <link> 태그: 외부 리소스 연결 (CSS 파일 포함)
웹 페이지에서 외부 스타일시트(CSS 파일) 를 연결할 때 사용한다.

<link rel="stylesheet" href="styles.css" />
rel="stylesheet" → 이 파일이 스타일시트(CSS) 임을 의미.
href="styles.css" → 연결할 CSS 파일의 경로.
웹 사이트에서 디자인을 변경할 때 CSS 파일을 수정하면 전체적인 스타일이 변경되므로, HTML과 CSS를 분리하는 것이 일반적이다.

8. <script> 태그: 외부 JavaScript 파일 연결
웹 페이지에서 JavaScript 파일을 불러와서 실행할 때 사용한다.

<script src="script.js" defer></script>
src="script.js" → 실행할 JavaScript 파일의 경로.
defer → HTML 문서가 완전히 로드된 후 JavaScript를 실행하도록 설정.
defer 속성을 사용하면, HTML이 모두 로드된 뒤에 스크립트가 실행되므로 웹 페이지의 로딩 속도를 최적화할 수 있다.

만약 이 속성이 없으면 HTML이 로딩되는 중간에 JavaScript가 실행되어 페이지 표시가 지연될 수 있다.

2.3. <body> 태그의 역할
<body> 태그는 HTML 문서에서 웹 페이지의 주요 콘텐츠를 포함하는 영역이다.
브라우저에 실제로 표시되는 모든 요소(텍스트, 이미지, 버튼, 링크 등)가 <body> 내부에 위치한다.

1. <body> 태그의 기본 구조
HTML 문서에서 <body> 태그는 <head> 태그 다음에 위치하며,
웹 페이지에서 사용자가 직접 볼 수 있는 내용을 포함한다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>게임 개발 블로그</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <h1>게임 개발 블로그에 오신 것을 환영합니다!</h1>
    <p>이곳에서는 HTML, CSS, JavaScript를 활용한 게임 개발 정보를 다룹니다.</p>
  </body>
</html>
위 HTML 코드에서 <body> 태그 내부에는 제목(h1)과 문단(p)이 포함되어 있으며,
브라우저에서 실행하면 사용자가 볼 수 있는 콘텐츠가 된다.

2. <body> 태그에 포함될 수 있는 주요 요소
<body> 내부에는 여러 가지 HTML 요소가 포함될 수 있다.
대표적으로 다음과 같은 요소들이 자주 사용된다.

요소	설명
<h1> ~ <h6>	제목(Heading) 태그
<p>	문단(Paragraph) 태그
<a>	하이퍼링크 태그
<img>	이미지 삽입 태그
<ul>, <ol>, <li>	목록(List) 태그
<table>	테이블(Table) 태그
<form>	사용자 입력 폼(Form) 태그
<button>	버튼 생성 태그
<div>, <span>	레이아웃을 구성하는 태그
즉, <body> 내부에는 텍스트, 이미지, 표, 버튼 등 다양한 요소가 포함될 수 있다.

3. <body> 태그의 스타일 지정
웹 페이지를 더 보기 좋게 꾸미기 위해 <body> 태그에 스타일을 적용할 수 있다.
이때, CSS를 사용하여 배경 색상, 글꼴, 여백 등을 조정할 수 있다.

다음은 배경 색상을 변경하고, 텍스트 정렬을 조정하는 예제이다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>게임 소개 페이지</title>
    <style>
      body {
        background-color: #1e1e1e; /* 배경 색상 */
        color: white; /* 글자 색상 */
        text-align: center; /* 텍스트 중앙 정렬 */
        font-family: Arial, sans-serif; /* 글꼴 스타일 */
      }
    </style>
  </head>
  <body>
    <h1>환영합니다!</h1>
    <p>
      이 웹사이트에서는 HTML과 CSS를 이용하여 게임 인터페이스를 만드는 방법을
      배울 수 있습니다.
    </p>
  </body>
</html>
background-color: #1e1e1e; → 검은색 배경 설정.
color: white; → 글자 색상을 흰색으로 설정.
text-align: center; → 텍스트를 중앙 정렬.
font-family: Arial, sans-serif; → 글꼴을 Arial 또는 기본 sans-serif 폰트로 설정.
이렇게 스타일을 지정하면 게임 소개 페이지의 디자인을 더욱 깔끔하게 정리할 수 있다.

4. <body> 태그 내에서 JavaScript 활용
<body> 태그 내부에서는 JavaScript를 사용하여 동적인 기능을 추가할 수 있다.
예를 들어, 버튼을 클릭하면 특정 메시지를 출력하는 기능을 추가할 수 있다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>게임 시작</title>
    <script>
      function startGame() {
        alert("게임을 시작합니다!");
      }
    </script>
  </head>
  <body>
    <h1>게임 대기 화면</h1>
    <button onclick="startGame()">게임 시작</button>
  </body>
</html>
<button> 태그를 사용하여 "게임 시작" 버튼을 추가.
onclick="startGame()" → 버튼을 클릭하면 startGame() 함수 실행.
alert("게임을 시작합니다!"); → 팝업(alert) 창을 띄우는 기능.
이 방식은 게임 개발에서 메뉴 화면을 구현할 때 유용하게 사용될 수 있다.

5. <body> 태그에서의 게임 개발 활용 예시
게임 개발을 할 때, <body> 태그 내부에서 Canvas API 또는 WebGL을 사용하여 그래픽을 그릴 수 있다.
아래는 <canvas> 태그를 활용하여 간단한 도형을 그리는 예제이다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>Canvas 게임 예제</title>
  </head>
  <body>
    <canvas id="gameCanvas" width="400" height="300"></canvas>

    <script>
      let canvas = document.getElementById("gameCanvas");
      let ctx = canvas.getContext("2d");

      // 파란색 사각형 그리기
      ctx.fillStyle = "blue";
      ctx.fillRect(50, 50, 100, 100);

      // 빨간색 원 그리기
      ctx.fillStyle = "red";
      ctx.beginPath();
      ctx.arc(250, 150, 50, 0, Math.PI * 2);
      ctx.fill();
    </script>
  </body>
</html>
<canvas> 태그를 추가하여 게임 화면을 표시할 공간을 생성.
getContext("2d") → 2D 그래픽을 그릴 수 있도록 설정.
fillRect(50, 50, 100, 100); → 파란색 사각형을 그림.
arc(250, 150, 50, 0, Math.PI * 2); → 빨간색 원을 그림.
이 방식은 HTML과 JavaScript를 활용한 간단한 2D 게임 개발에 매우 유용하다.
이를 확장하면 플레이어 캐릭터, 적 캐릭터, 배경 등의 그래픽을 추가하여 더 복잡한 게임을 만들 수도 있다.

학습자의 사고를 돕기 위한 질문
웹 문서에서 <body> 태그 내부에 어떤 요소들이 포함될 수 있는가?

사용자가 실제로 볼 수 있는 콘텐츠의 종류를 생각해보라.
HTML 문서에서 <body> 태그를 생략하면 어떤 문제가 발생할 수 있는가?

브라우저의 기본 동작을 고려하여 설명해보라.
실습 문제
문제 1: <body> 태그 활용하기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<h1> 태그를 사용하여 제목을 "내 첫 번째 웹 페이지"로 설정한다.
<p> 태그를 사용하여 소개 문장을 작성한다.
<img> 태그를 사용하여 이미지를 삽입한다.
<a> 태그를 사용하여 "자세히 보기" 링크를 추가한다.
3. 텍스트 관련 태그
3.1. 제목 태그 (<h1> ~ <h6>)
제목 태그(<h1> ~ <h6>)는 HTML 문서에서 텍스트의 계층 구조를 정의하는 역할을 한다.
제목 태그는 문서의 논리적 구조를 명확히 하고, 검색 엔진 최적화(SEO) 에도 영향을 미친다.

1. 제목 태그의 기본 개념
HTML에서는 <h1>부터 <h6>까지 총 6단계의 제목 태그가 제공된다.

<h1>은 가장 중요한 제목을 의미하며, 문서의 주요 제목에 사용된다.
<h6>은 가장 작은 제목으로, 부가적인 소제목에 사용될 수 있다.
다음은 각 제목 태그의 크기 비교 예제이다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>제목 태그 예제</title>
  </head>
  <body>
    <h1>게임 개발을 위한 HTML</h1>
    <h2>HTML의 역할</h2>
    <h3>HTML의 기본 구조</h3>
    <h4>태그의 종류</h4>
    <h5>텍스트 관련 태그</h5>
    <h6>제목 태그 사용 예시</h6>
  </body>
</html>
위 코드를 실행하면 <h1>부터 <h6>까지 제목이 크기 순서대로 표시된다.

2. 제목 태그의 시각적 크기
브라우저에서는 기본적으로 제목 태그의 크기를 아래와 같이 설정한다.

제목 태그	기본 글자 크기(px)	굵기 (기본값)
<h1>	32px	bold
<h2>	24px	bold
<h3>	18.72px	bold
<h4>	16px	bold
<h5>	13.28px	bold
<h6>	10.72px	bold
하지만, CSS를 사용하여 글자 크기를 조절할 수 있다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>제목 스타일 변경</title>
    <style>
      h1 {
        font-size: 40px;
        color: blue;
      }
      h2 {
        font-size: 30px;
        color: green;
      }
      h3 {
        font-size: 25px;
        color: red;
      }
    </style>
  </head>
  <body>
    <h1>게임 인터페이스 디자인</h1>
    <h2>UI 요소의 구성</h2>
    <h3>버튼과 텍스트 스타일</h3>
  </body>
</html>
<h1>: 크기를 40px, 색상을 파란색(blue) 으로 변경.
<h2>: 크기를 30px, 색상을 초록색(green) 으로 변경.
<h3>: 크기를 25px, 색상을 빨간색(red) 으로 변경.
3. 제목 태그와 검색 엔진 최적화(SEO)
제목 태그는 SEO(Search Engine Optimization, 검색 엔진 최적화)에 중요한 역할을 한다.

<h1> 태그는 문서에서 한 번만 사용하는 것이 일반적이며, 문서의 핵심 내용을 포함해야 한다.
<h2> ~ <h6> 태그는 부제목 및 내용을 구조화하는 데 사용한다.
검색 엔진(예: Google)은 제목 태그를 분석하여 페이지의 주요 주제를 판단한다.
예를 들어, 게임 개발 블로그의 제목 구조는 다음과 같이 구성할 수 있다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>게임 개발 가이드</title>
  </head>
  <body>
    <h1>게임 개발 기초 가이드</h1>
    <h2>1. 게임 개발을 위한 필수 기술</h2>
    <h3>1.1. 프로그래밍 언어</h3>
    <h3>1.2. 게임 엔진</h3>

    <h2>2. HTML과 웹 게임 개발</h2>
    <h3>2.1. HTML5 Canvas 활용</h3>
    <h3>2.2. JavaScript와 게임 로직</h3>
  </body>
</html>
이와 같은 구조를 가지면 검색 엔진이 페이지의 주요 내용과 계층 구조를 쉽게 이해할 수 있다.

4. 제목 태그의 올바른 사용
제목 태그를 사용할 때는 올바른 계층 구조를 유지하는 것이 중요하다.

좋은 예제 (계층 구조 유지)

<h1>게임 개발 가이드</h1>
<h2>1. 게임 프로그래밍</h2>
<h3>1.1. JavaScript 활용</h3>
<h3>1.2. WebGL과 3D 그래픽</h3>
<h2>2. 게임 디자인 원칙</h2>
<h3>2.1. UI/UX 개념</h3>
나쁜 예제 (제목 순서가 혼란스러움)

<h1>게임 개발 가이드</h1>
<h3>1. 게임 프로그래밍</h3>
<h2>1.1. JavaScript 활용</h2>
<h5>1.2. WebGL과 3D 그래픽</h5>
<h1>2. 게임 디자인 원칙</h1>
위와 같은 잘못된 사용은 검색 엔진과 사용자가 문서의 구조를 이해하는 데 혼란을 줄 수 있다.

5. 제목 태그를 활용한 게임 개발 예제
웹에서 게임 내 HUD(Head-Up Display) 또는 UI 구성에도 제목 태그를 활용할 수 있다.

다음은 HTML과 CSS를 사용하여 게임 내 메뉴를 구성하는 예제이다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>게임 메뉴 UI</title>
    <style>
      body {
        background-color: black;
        color: white;
        text-align: center;
        font-family: Arial, sans-serif;
      }
      h1 {
        font-size: 36px;
        color: yellow;
      }
      h2 {
        font-size: 28px;
        color: lightblue;
      }
      h3 {
        font-size: 22px;
        color: lightgreen;
      }
    </style>
  </head>
  <body>
    <h1>게임 시작</h1>
    <h2>메인 메뉴</h2>
    <h3>▶ 새로운 게임</h3>
    <h3>▶ 이어하기</h3>
    <h3>▶ 설정</h3>
  </body>
</html>
<h1> → 게임 타이틀 ("게임 시작")
<h2> → 메뉴 카테고리 ("메인 메뉴")
<h3> → 실제 메뉴 항목 ("새로운 게임", "이어하기", "설정")
이렇게 제목 태그를 활용하면 게임 내 UI를 구성하는 데에도 유용하게 사용할 수 있다.

학습자의 사고를 돕기 위한 질문
HTML에서 <h1>부터 <h6>까지의 태그는 각각 어떤 용도로 사용되는가?

제목의 계층 구조와 검색 엔진 최적화를 고려해보라.
웹 접근성을 고려할 때, 제목 태그를 적절하게 배치하는 것이 중요한 이유는 무엇인가?

스크린 리더를 사용하는 사용자 입장에서 생각해보라.
실습 문제
문제 1: 제목 태그 사용하기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<h1> 태그를 사용하여 웹사이트의 대표 제목을 작성한다.
<h2> 태그를 사용하여 주요 섹션 제목을 추가한다.
<h3> 태그를 사용하여 세부 항목을 추가한다.
모든 제목 태그를 사용하여 계층적으로 문서를 구성한다.
3.2. 단락 태그 (<p>)
HTML에서 <p> 태그는 단락(paragraph)을 정의하는 요소이다.
웹 문서에서 문장을 논리적으로 구분하고, 가독성을 높이는 역할을 한다.
또한, <p> 태그를 사용하면 브라우저가 자동으로 위아래 여백(margin)을 추가하여 단락 간의 간격을 조절해준다.

1. 단락 태그의 기본 사용법
HTML 문서에서 <p> 태그를 사용하면 한 문단을 생성할 수 있다.
다음은 기본적인 <p> 태그 사용 예제이다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>단락 태그 예제</title>
  </head>
  <body>
    <p>이것은 첫 번째 단락입니다.</p>
    <p>이것은 두 번째 단락입니다.</p>
  </body>
</html>
위 코드를 실행하면 두 개의 단락이 생성되며, 브라우저는 기본적으로 각 단락 사이에 공백을 자동으로 추가한다.

2. 단락 태그의 기본 스타일
웹 브라우저는 <p> 태그에 기본적으로 위아래 여백(margin) 을 추가한다.
기본적인 스타일은 다음과 같다.

속성	기본값
display	block (블록 요소)
margin-top	16px
margin-bottom	16px
line-height	1.5 (줄 간격)
이 기본 스타일을 CSS를 사용하여 변경할 수 있다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>단락 스타일 변경</title>
    <style>
      p {
        color: darkblue;
        font-size: 18px;
        line-height: 1.8;
        margin-bottom: 20px;
      }
    </style>
  </head>
  <body>
    <p>이 단락은 파란색으로 표시되며, 글자 크기가 18px로 설정되었습니다.</p>
    <p>줄 간격이 넓어지고, 단락 사이의 여백이 20px로 설정되었습니다.</p>
  </body>
</html>
이제 <p> 태그가 적용된 단락의 글자 색상은 파란색(darkblue) 으로 변경되고,
글자 크기(18px) , 줄 간격(1.8) , 단락 사이 여백(20px) 이 조정된다.

3. 단락 태그 내에서 줄바꿈 처리
HTML에서 줄바꿈을 하려면 <br> 태그를 사용해야 한다.
<p> 태그 내부에서 Enter를 눌러도 줄바꿈이 적용되지 않는다.

<p>이 문장은 줄바꿈 없이 표시됩니다.</p>
<p>이 문장은<br />줄바꿈이 적용되었습니다.</p>
위 코드를 실행하면 두 번째 단락에서 <br> 태그가 적용된 부분에서 줄바꿈이 일어난다.

4. <p> 태그와 다른 블록 요소와의 관계
<p> 태그는 블록 요소(block element) 이므로 다른 블록 요소(<div>, <section> 등)와 함께 사용할 때 주의해야 한다.
HTML에서는 <p> 태그 내부에 다른 블록 요소를 포함할 수 없다.

잘못된 예제 (블록 요소 포함 오류)

<p>이 단락 안에 <div>블록 요소</div>를 포함하면 오류가 발생합니다.</p>
올바른 예제

<p>이 단락 안에서는 <span>인라인 요소</span>만 사용할 수 있습니다.</p>
5. <p> 태그를 활용한 게임 개발 관련 예제
게임 개발에서 <p> 태그는 게임 설명, 튜토리얼, 대사(Dialog), UI 요소 등에 활용될 수 있다.

다음은 HTML과 CSS를 이용해 게임의 대사 창을 구현하는 예제이다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>게임 대사 창</title>
    <style>
      .dialog-box {
        width: 400px;
        padding: 20px;
        background-color: rgba(0, 0, 0, 0.8);
        color: white;
        border-radius: 10px;
        font-size: 18px;
        line-height: 1.5;
        margin: 20px auto;
        text-align: center;
      }
    </style>
  </head>
  <body>
    <div class="dialog-box">
      <p>"이곳은 마법의 숲... 네가 찾던 비밀이 이곳에 있을지도 몰라."</p>
    </div>
  </body>
</html>
.dialog-box : 게임의 대사 창을 표현하는 컨테이너.
배경색(rgba(0,0,0,0.8)) : 반투명한 검은색 배경.
글자색(color: white) : 흰색으로 설정하여 가독성을 높임.
둥근 테두리(border-radius: 10px) : 부드러운 모서리 표현.
가운데 정렬(margin: 20px auto) : 대사 창이 화면 중앙에 오도록 설정.
이와 같이 <p> 태그를 활용하면 게임 내 텍스트 기반 UI를 구성할 수 있다.

6. <p> 태그를 활용한 HTML5 게임 요소
HTML5에서는 Canvas API와 함께 <p> 태그를 활용하여 UI를 만들 수도 있다.
다음은 점수(score) UI를 구성하는 예제이다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>게임 점수 UI</title>
    <style>
      #score-board {
        font-size: 24px;
        font-weight: bold;
        color: white;
        background-color: black;
        padding: 10px;
        width: 150px;
        text-align: center;
        border-radius: 5px;
        position: absolute;
        top: 20px;
        left: 20px;
      }
    </style>
  </head>
  <body>
    <p id="score-board">Score: 0</p>

    <script>
      let score = 0;
      function increaseScore() {
        score += 10;
        document.getElementById("score-board").innerText = "Score: " + score;
      }

      // 3초마다 점수를 증가시키는 예제
      setInterval(increaseScore, 3000);
    </script>
  </body>
</html>
<p> 태그로 점수판을 생성하고 id="score-board"로 지정.
CSS로 점수판의 디자인을 구성(검은 배경, 흰색 텍스트, 중앙 정렬).
JavaScript를 사용하여 innerText 속성을 변경, 3초마다 점수가 증가하도록 설정.
이처럼 <p> 태그는 게임 UI에서 점수판, 대화 창, 설명 문구 등 다양한 용도로 활용될 수 있다.

학습자의 사고를 돕기 위한 질문
HTML에서 <p> 태그가 존재하는 이유는 무엇인가?

문서의 가독성과 콘텐츠 구성의 중요성을 고려해보라.
줄바꿈 없이 텍스트를 구분할 때 <p> 태그 대신 사용할 수 있는 방법은 무엇인가?

CSS를 활용한 스타일링 기법을 떠올려보라.
실습 문제
문제 1: 단락 태그 활용하기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<p> 태그를 사용하여 문단을 나눈다.
한 문단에는 자기소개 내용을 작성한다.
다른 문단에는 자신의 취미에 대한 설명을 추가한다.
<br> 태그를 사용하지 않고 문단을 구분한다.
3.3. 줄바꿈 및 구분선
HTML 문서에서 줄바꿈을 적용하거나 구분선을 삽입하는 방법은 여러 가지가 있다.
주로 <br> 태그를 사용하여 줄바꿈을 하고, <hr> 태그를 사용하여 구분선을 삽입할 수 있다.
이 태그들은 웹 페이지의 가독성을 높이고, 문서를 더 구조적으로 구성하는 데 중요한 역할을 한다.

1. <br> 태그: 줄바꿈 (Line Break)
<br> 태그는 HTML에서 줄바꿈을 강제로 적용할 때 사용된다.
이 태그는 "Self-closing tag" (닫는 태그가 없는 태그) 로, <br>만 입력하면 동작한다.

<p>이 문장은 줄바꿈 없이 표시됩니다.</p>
<p>이 문장에는<br />줄바꿈이 적용됩니다.</p>
위 코드를 실행하면 첫 번째 단락은 그대로 출력되지만,
두 번째 단락에서는 <br> 태그가 삽입된 위치에서 줄바꿈이 발생한다.

2. <br> 태그를 활용한 여러 줄 텍스트
<br> 태그를 사용하면 여러 줄에 걸쳐 문장을 표시할 수 있다.

<p>
  HTML에서 줄바꿈을 하려면 <br />
  이렇게 <br />
  <br />
  여러 개의 <br />
  태그를 사용하면 된다.
</p>
위 코드를 실행하면 <br>이 들어간 위치에서 줄바꿈이 일어나면서 문장이 여러 줄로 출력된다.

하지만 단락 간 간격을 조정하기 위해 <br> 태그를 여러 개 사용하는 것은 좋은 방법이 아니다.
CSS의 margin 또는 padding 속성을 사용하여 더 정교하게 조정하는 것이 권장된다.

3. <br> 태그를 사용한 게임 개발 예제
게임 개발에서는 <br> 태그를 대화(Dialog) 시스템이나 튜토리얼 안내문을 작성할 때 활용할 수 있다.
다음은 게임 내 캐릭터 대사창을 HTML과 CSS로 구성하는 예제이다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>게임 대화창</title>
    <style>
      .dialog-box {
        width: 400px;
        padding: 15px;
        background-color: rgba(0, 0, 0, 0.8);
        color: white;
        border-radius: 8px;
        font-size: 16px;
        line-height: 1.5;
        margin: 20px auto;
        text-align: center;
      }
    </style>
  </head>
  <body>
    <div class="dialog-box">
      <p>
        "어서 와, 용사여!<br />
        이곳은 신비로운 마법의 숲이다.<br />
        네가 찾던 보물이 이곳에 숨겨져 있다."
      </p>
    </div>
  </body>
</html>
위 코드에서는 <br> 태그를 이용하여 게임 내 대사에 줄바꿈을 적용했다.
이와 같이 <br> 태그를 활용하면 플레이어에게 제공하는 정보나 스토리텔링을 효과적으로 구성할 수 있다.

4. <hr> 태그: 구분선 (Horizontal Rule)
<hr> 태그는 수평선(horizontal rule)을 삽입하여 문서를 논리적으로 구분할 때 사용된다.
이 태그 또한 <br> 태그와 마찬가지로 닫는 태그 없이 단독으로 사용된다.

<p>이 문장은 구분선 위에 있습니다.</p>
<hr />
<p>이 문장은 구분선 아래에 있습니다.</p>
위 코드를 실행하면 가로 줄이 문서에 삽입되어, 두 개의 문장을 분리하는 역할을 한다.

5. <hr> 태그의 기본 스타일
브라우저는 기본적으로 <hr> 태그에 아래와 같은 스타일을 적용한다.

속성	기본값
display	block (블록 요소)
border	없음
height	1px
width	100% (컨테이너의 전체 너비)
margin	8px 0
background-color	gray
6. <hr> 태그의 스타일 변경
CSS를 사용하여 <hr> 태그의 색상, 두께, 스타일을 변경할 수 있다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>구분선 스타일</title>
    <style>
      .custom-hr {
        border: none;
        height: 4px;
        background-color: darkblue;
        width: 50%;
        margin: 20px auto;
      }
    </style>
  </head>
  <body>
    <p>이 문장은 구분선 위에 있습니다.</p>
    <hr class="custom-hr" />
    <p>이 문장은 구분선 아래에 있습니다.</p>
  </body>
</html>
위 코드에서 <hr> 태그를 커스텀 스타일링하여 진한 파란색, 두께 4px, 가로 길이 50% 로 조정했다.
이렇게 하면 문서 내에서 강조할 필요가 있는 부분을 시각적으로 분리하는 역할을 할 수 있다.

7. <hr> 태그를 활용한 게임 UI
게임 개발에서는 <hr> 태그를 활용하여 메뉴 구분, 상태창(UI) 구분, 로그(log) 출력 등에 사용할 수 있다.
다음은 게임의 전투 로그를 구분하는 예제이다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>전투 로그</title>
    <style>
      .log-container {
        width: 400px;
        padding: 15px;
        background-color: black;
        color: limegreen;
        font-size: 14px;
        border-radius: 8px;
        margin: 20px auto;
      }
      hr {
        border: none;
        height: 2px;
        background-color: limegreen;
      }
    </style>
  </head>
  <body>
    <div class="log-container">
      <p>몬스터가 나타났다!</p>
      <hr />
      <p>플레이어가 검으로 공격했다! (데미지: 12)</p>
      <hr />
      <p>몬스터가 반격했다! (데미지: 8)</p>
    </div>
  </body>
</html>
전투 로그 UI를 구성할 때, <hr> 태그를 사용하여 각 로그를 구분할 수 있다.
검은 배경과 초록색 텍스트로 고전적인 콘솔 스타일의 UI를 표현했다.
공격, 반격, 이벤트 로그를 명확하게 구분하여 가독성을 높였다.
이처럼 <hr> 태그는 단순한 구분선 이상의 역할을 하며, 게임 UI에서도 유용하게 활용될 수 있다.

학습자의 사고를 돕기 위한 질문
<br> 태그와 <p> 태그를 사용할 때, 각각의 차이점은 무엇인가?

줄바꿈의 의미와 문단 구분의 차이를 생각해보라.
<hr> 태그를 문서에서 사용하면 어떤 효과가 있는가?

문서의 섹션을 시각적으로 구분하는 방식에 대해 생각해보라.
실습 문제
문제 1: 줄바꿈과 구분선 적용하기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<p> 태그를 사용하여 두 개의 문단을 작성한다.
두 문단 사이에 <hr> 태그를 추가하여 구분한다.
문단 내에서 <br> 태그를 사용하여 줄바꿈을 추가한다.
3.4. 강조 태그
HTML에서 특정 텍스트를 강조하기 위해 <strong> 태그와 <em> 태그를 사용한다.
이 태그들은 사용자의 가독성을 높이고, 의미적으로 중요한 정보를 강조하는 역할을 한다.
검색 엔진 최적화(SEO)에도 영향을 미치므로 올바르게 사용해야 한다.

1. <strong> 태그: 강한 강조 (Bold Text)
<strong> 태그는 텍스트를 중요하게 강조할 때 사용한다.
기본적으로 브라우저에서 굵게(bold) 표시되며, 검색 엔진은 이 태그를 감싸고 있는 텍스트를 중요하게 인식한다.

<p>일반적인 텍스트입니다.</p>
<p><strong>이 부분은 중요한 정보입니다.</strong></p>
위 코드를 실행하면, <strong> 태그로 감싼 텍스트가 굵게 표시된다.

SEO 관점에서의 활용
검색 엔진 최적화(SEO)에서 <strong> 태그는 웹 페이지 내 중요한 키워드를 강조하는 역할을 한다.
따라서 페이지 내에서 가장 중요한 키워드에만 사용해야 한다.

<p>
  이 게임의 <strong>보스 몬스터</strong>는 매우 강력하며,
  <strong>전략적인 플레이</strong>가 필요합니다.
</p>
위와 같이 보스 몬스터와 전략적인 플레이 같은 중요한 키워드를 강조하면 검색 엔진이 이를 더 중요하게 인식할 수 있다.

2. <em> 태그: 강조 (Italic Text)
<em> 태그는 특정 텍스트를 기울임체(italic) 로 표시하며, 강조된 의미를 전달하는 역할을 한다.
<strong>보다는 덜 중요하지만, 문장 내에서 강조할 부분을 부각하는 데 유용하다.

<p>이 게임에서는 <em>전략적인 판단</em>이 중요합니다.</p>
위 코드를 실행하면 <em> 태그로 감싼 "전략적인 판단"이 기울임체로 표시된다.

의미론적 차이

<strong>은 강한 강조로, 검색 엔진이 이 부분이 중요한 정보라고 인식한다.
<em>은 일반 강조로, 사용자에게 강조된 의미를 전달하지만 검색 엔진에는 <strong>만큼 영향을 미치지 않는다.
3. <strong>과 <em>을 함께 사용하기
둘 다 동시에 사용할 수도 있다.
예를 들어, 강한 강조와 일반 강조를 조합하여 더욱 뚜렷한 강조 효과를 낼 수 있다.

<p>
  <strong><em>이 아이템은 매우 희귀합니다!</em></strong>
</p>
위 코드를 실행하면, "이 아이템은 매우 희귀합니다!"가 굵은 기울임체로 표시된다.
이는 게임 내에서 특별한 아이템이나 중요한 공지사항을 강조할 때 유용하다.

4. <b>와 <i> 태그와의 차이점
HTML에는 <b>(bold)와 <i>(italic) 태그도 있다.
그러나 <strong>과 <em> 태그와는 기능적 차이가 있다.

태그	역할	의미론적 의미(SEO)	스타일
<strong>	중요한 정보 강조	O (검색 엔진이 중요하게 인식)	굵게 표시
<em>	텍스트 강조	O (일반 강조)	기울임 표시
<b>	단순한 굵은 글씨	X (SEO 영향 없음)	굵게 표시
<i>	단순한 기울임체	X (SEO 영향 없음)	기울임 표시
<b>와 <i>는 단순한 스타일링 태그이며, 의미적으로 중요한 텍스트를 강조하는 역할을 하지 않는다.
검색 엔진이 <b>와 <i> 태그로 감싼 텍스트를 특별히 중요하게 인식하지 않는다.

5. 게임 개발에서의 활용 예제
게임 개발에서는 <strong>과 <em>을 대화창, 공지사항, 시스템 메시지 등에 활용할 수 있다.

다음은 게임 내 시스템 메시지를 표시하는 예제이다.

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>게임 시스템 메시지</title>
    <style>
      .message-box {
        width: 400px;
        padding: 15px;
        background-color: black;
        color: white;
        border-radius: 8px;
        font-size: 16px;
        line-height: 1.5;
        margin: 20px auto;
        text-align: center;
      }
      .warning {
        color: red;
        font-weight: bold;
      }
      .important {
        font-style: italic;
        color: yellow;
      }
    </style>
  </head>
  <body>
    <div class="message-box">
      <p>
        <strong class="warning">경고!</strong>
        <em class="important">체력이 부족합니다.</em>
      </p>
      <p>포션을 사용하여 체력을 회복하세요.</p>
    </div>
  </body>
</html>
이 코드에서는:

<strong> 태그를 사용하여 경고 메시지("경고!") 를 강조했다.
<em> 태그를 사용하여 중요한 정보("체력이 부족합니다.") 를 강조했다.
CSS를 활용하여 경고 메시지는 빨간색, 중요한 정보는 노란색으로 표시했다.
이와 같은 방식으로 <strong>과 <em> 태그를 조합하면, 게임 내 인터페이스(UI)에서 중요한 정보를 효과적으로 전달할 수 있다.

학습자의 사고를 돕기 위한 질문
<strong> 태그와 <em> 태그의 차이점은 무엇인가?

검색 엔진 최적화(SEO)와 접근성 측면에서의 차이를 고려해보라.
텍스트를 강조하는 방법으로 CSS 스타일링 대신 HTML 태그를 사용하는 이유는 무엇인가?

의미론적 마크업의 중요성을 떠올려보라.
실습 문제
문제 1: 강조 태그 적용하기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<strong> 태그를 사용하여 중요한 단어를 강조한다.
<em> 태그를 사용하여 특정 문장을 기울임 처리한다.
두 태그를 적절히 조합하여 가독성을 높인다.
4. 하이퍼링크 및 이미지 삽입
4.1. 하이퍼링크 생성 (<a>)
하이퍼링크는 HTML에서 다른 웹 페이지, 문서, 이메일 또는 동일한 페이지 내 특정 위치로 이동할 수 있도록 도와주는 요소이다.
이 기능을 제공하는 태그가 <a>(anchor) 태그이며, 웹 페이지를 구성하는 데 필수적인 요소 중 하나이다.

1. 기본적인 하이퍼링크 생성
<a> 태그를 사용하여 외부 웹사이트로 연결하는 방법은 다음과 같다.

<a href="https://www.example.com">Example 웹사이트로 이동</a>
이 코드를 실행하면 "Example 웹사이트로 이동"이라는 텍스트가 링크로 표시되며, 클릭하면 https://www.example.com으로 이동한다.
여기서 href 속성은 이동할 URL을 지정하는 역할을 한다.

2. 내부 링크와 외부 링크
내부 링크: 같은 웹사이트 내 다른 페이지로 이동
외부 링크: 다른 웹사이트로 이동
<!-- 내부 링크 -->
<a href="about.html">회사 소개 페이지로 이동</a>

<!-- 외부 링크 -->
<a href="https://www.google.com">구글로 이동</a>
내부 링크는 같은 도메인 내에서 이동할 때 사용하며,
외부 링크는 다른 웹사이트로 이동할 때 사용된다.

3. 새 창에서 링크 열기 (target="_blank")
기본적으로 <a> 태그는 클릭하면 현재 창에서 링크를 연다.
그러나 target="_blank" 속성을 사용하면 새로운 탭에서 링크를 열 수 있다.

<a href="https://www.naver.com" target="_blank">네이버 새 창에서 열기</a>
이 속성을 사용하면 사용자가 현재 페이지를 유지한 채 새로운 창에서 페이지를 확인할 수 있어 편리하다.
특히 외부 사이트로 연결할 때 유용하다.

4. 특정 위치로 이동하는 앵커 링크
같은 페이지 내에서 특정 위치로 이동하고 싶을 때 <a> 태그를 사용할 수 있다.
이 경우, id 속성과 함께 사용하면 된다.

<!-- 특정 위치로 이동할 앵커 링크 -->
<a href="#section3">섹션 3으로 이동</a>

<!-- 이동할 목적지 -->
<h2 id="section3">여기가 섹션 3</h2>
위 코드를 실행하면, "섹션 3으로 이동" 링크를 클릭했을 때 해당 위치로 스크롤이 이동하게 된다.
이 기능은 긴 페이지에서 내비게이션을 만들 때 유용하다.

5. 이메일 및 전화번호 링크
웹 페이지에서 특정 이메일 주소나 전화번호로 바로 연결하는 것도 가능하다.
이때 mailto: 또는 tel: 프로토콜을 사용한다.

<!-- 이메일 보내기 -->
<a href="mailto:example@email.com">이메일 보내기</a>

<!-- 전화 걸기 -->
<a href="tel:+821012345678">전화 걸기</a>
mailto:를 사용하면 이메일 앱이 열리고, 자동으로 해당 주소가 입력된다.
tel:을 사용하면 모바일 기기에서 바로 전화를 걸 수 있다.
6. 버튼 형태의 링크 만들기
기본적으로 <a> 태그는 텍스트 형태의 링크를 제공하지만, CSS를 사용하면 버튼처럼 스타일링할 수도 있다.

<style>
  .link-button {
    display: inline-block;
    padding: 10px 20px;
    background-color: #3498db;
    color: white;
    text-decoration: none;
    border-radius: 5px;
    font-size: 16px;
  }
</style>

<a href="https://www.example.com" class="link-button">웹사이트 방문</a>
이 코드를 실행하면, 파란색 배경과 흰색 텍스트를 가진 버튼 형태의 링크가 생성된다.

7. 게임 개발에서의 활용
게임 개발에서 <a> 태그는 다양한 용도로 사용될 수 있다.

예제 1: 게임 내 공지사항 페이지 연결

<a href="notice.html">공지사항 확인</a>
게임 웹사이트에서 새로운 패치 노트나 이벤트 정보를 확인할 수 있도록 제공할 수 있다.

예제 2: 다운로드 링크

<a href="game_installer.exe" download>게임 다운로드</a>
이 코드를 사용하면 게임 설치 파일을 다운로드할 수 있는 링크를 제공할 수 있다.

예제 3: HTML5 기반 게임 내 메뉴

<a href="game.html" class="link-button">게임 시작</a>
HTML5와 JavaScript로 만든 게임에서 메인 메뉴에서 게임 시작 버튼을 만들 때 활용할 수 있다.

학습자의 사고를 돕기 위한 질문
<a> 태그를 사용할 때 href 속성이 하는 역할은 무엇인가?

링크의 목적과 URL의 관계를 고려해보라.
target="_blank" 속성을 사용하면 어떤 효과가 발생하는가?

사용자 경험과 브라우저 동작을 생각해보라.
실습 문제
문제 1: 하이퍼링크 생성하기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<a> 태그를 사용하여 "네이버" 홈페이지(https://www.naver.com)로 이동하는 링크를 만든다.
링크 클릭 시 새 창에서 열리도록 target="_blank" 속성을 추가한다.
내부 링크를 생성하여 같은 페이지 내 특정 섹션으로 이동할 수 있도록 설정한다.
4.2. 이미지 삽입 (<img>)
이미지는 웹 페이지에서 필수적인 요소 중 하나로, 콘텐츠를 시각적으로 보강하고 사용자의 이해도를 높이는 데 중요한 역할을 한다.
HTML에서는 <img> 태그를 사용하여 이미지를 삽입하며, 다양한 속성을 활용하여 크기 조정, 대체 텍스트 지정, 레이아웃 조정을 수행할 수 있다.

1. 기본적인 이미지 삽입
HTML에서 이미지를 삽입할 때는 <img> 태그를 사용하며, src(source) 속성을 이용하여 이미지의 경로를 지정한다.

<img src="example.jpg" />
위 코드는 example.jpg라는 이미지 파일을 페이지에 표시한다.
이미지의 크기나 대체 텍스트 없이 기본적인 형태로 삽입된다.

2. src 속성과 이미지 경로
이미지 파일의 위치에 따라 src 속성의 값이 달라진다.

절대 경로: 이미지가 다른 웹 서버에 있을 경우 URL을 입력한다.

<img src="https://www.example.com/images/logo.png" />
상대 경로: 현재 문서를 기준으로 특정 디렉토리에 있는 이미지를 불러온다.

<img src="images/logo.png" />
루트 경로 (/) 사용: 웹 서버의 루트 디렉토리를 기준으로 이미지를 불러온다.

<img src="/assets/logo.png" />
3. alt 속성: 대체 텍스트
웹 접근성을 위해 alt(alternative text) 속성을 제공해야 한다.
이 속성은 이미지를 불러오지 못했을 때 표시될 텍스트이며, 스크린 리더를 사용하는 사용자에게도 중요한 정보가 된다.

<img src="avatar.png" alt="사용자 프로필 이미지" />
이미지가 정상적으로 로드되지 않을 경우 "사용자 프로필 이미지" 라는 텍스트가 대신 표시된다.
검색 엔진 최적화(SEO)에도 기여하며, 시각 장애인을 위한 웹 접근성을 높이는 역할을 한다.
4. 이미지 크기 조정 (width, height)
이미지의 크기는 width(가로), height(세로) 속성을 통해 조절할 수 있다.

<img src="character.png" alt="게임 캐릭터" width="200" height="300" />
위 코드는 가로 200px, 세로 300px 크기의 이미지를 표시한다.

비율을 유지하면서 크기를 조정하려면 한쪽 값만 지정하고, 다른 한쪽은 자동 조정되도록 한다.

<img src="character.png" alt="게임 캐릭터" width="200" />
CSS를 이용한 크기 조정도 가능하다.

<style>
  .game-logo {
    width: 100px;
    height: auto;
  }
</style>

<img src="logo.png" class="game-logo" />
위 예제에서 height: auto;를 사용하면 이미지의 원본 비율이 유지된 채로 가로 크기만 조정된다.

5. 이미지 경계선 제거
HTML 4 이전에는 <img> 태그에 border 속성을 추가하여 이미지에 테두리를 적용할 수 있었으나,
현재는 CSS를 활용하는 것이 일반적이다.

<style>
  .no-border {
    border: none;
  }
</style>

<img src="button.png" class="no-border" />
기본적으로 <img> 태그는 하이퍼링크(<a>) 내에 포함될 경우 테두리가 생길 수 있으므로, CSS를 사용하여 테두리를 제거해야 한다.
6. 배경 이미지와의 차이
이미지를 삽입할 때 HTML <img> 태그를 사용할 수도 있고, CSS의 background-image 속성을 사용할 수도 있다.

<img> 태그를 사용할 경우:

<img src="character.png" alt="게임 캐릭터" />
CSS의 background-image를 사용할 경우:

<style>
  .background-container {
    width: 300px;
    height: 200px;
    background-image: url("background.jpg");
    background-size: cover;
  }
</style>

<div class="background-container"></div>
<img> 태그는 문서의 콘텐츠로 인식되지만, background-image는 스타일 요소로 사용된다.

7. 게임 개발에서의 활용
웹 게임이나 게임 관련 웹사이트에서도 <img> 태그는 다양한 방식으로 활용된다.

예제 1: 게임 내 캐릭터 스프라이트 표시

<img src="character.png" alt="플레이어 캐릭터" width="150" />
게임의 캐릭터 이미지를 불러와 화면에 표시하는 데 사용할 수 있다.

예제 2: 게임 UI에서 버튼으로 활용

<a href="start.html">
  <img src="start-button.png" alt="게임 시작 버튼" />
</a>
이렇게 하면 버튼을 이미지로 표현할 수 있으며, 클릭 시 새로운 페이지로 이동하도록 할 수 있다.

예제 3: 아이템 정보 표시

<img src="sword.png" alt="전설의 검" title="전설의 검: 공격력 +10" />
title 속성을 추가하면 마우스를 올렸을 때 툴팁으로 정보를 제공할 수도 있다.

학습자의 사고를 돕기 위한 질문
웹 페이지에서 <img> 태그의 alt 속성이 중요한 이유는 무엇인가?

접근성과 SEO 최적화 측면에서 고려해보라.
이미지 파일을 로드할 때 경로 설정이 잘못되면 어떻게 되는가?

절대 경로와 상대 경로를 비교하여 설명해보라.
실습 문제
문제 1: 이미지 삽입하기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<img> 태그를 사용하여 이미지를 삽입한다.
src 속성을 사용하여 images/sample.jpg 경로의 이미지를 불러온다.
alt 속성을 설정하여 "샘플 이미지"라는 설명을 추가한다.
이미지의 너비를 300px로 조정한다.
5. 목록 태그 (리스트 요소)
5.1. 순서 없는 목록 (<ul>, <li>)
HTML에서 순서 없는 목록(Unordered List)은 <ul> 태그와 <li>(List Item) 태그를 사용하여 생성한다.
순서가 중요하지 않은 항목을 나열할 때 사용하며, 기본적으로 각 항목 앞에 점(•)이 표시된다.

1. 기본적인 순서 없는 목록
다음은 <ul> 태그와 <li> 태그를 이용한 기본적인 목록 예제이다.

<ul>
  <li>게임 캐릭터 선택</li>
  <li>아이템 구매</li>
  <li>퀘스트 수행</li>
</ul>
위 코드를 브라우저에서 실행하면 다음과 같은 목록이 출력된다.

게임 캐릭터 선택
아이템 구매
퀘스트 수행
각 항목 앞에는 기본 스타일의 점(•)이 표시된다.

2. 목록 기호 변경
기본적으로 <ul> 태그의 목록 기호는 검은 원 (•) 이지만, CSS의 list-style-type 속성을 사용하여 다양한 스타일로 변경할 수 있다.

<style>
  .square-list {
    list-style-type: square;
  }
  .circle-list {
    list-style-type: circle;
  }
  .none-list {
    list-style-type: none;
  }
</style>

<ul class="square-list">
  <li>스퀘어 스타일 목록</li>
  <li>각 항목 앞에 ■ 표시</li>
</ul>

<ul class="circle-list">
  <li>원형 스타일 목록</li>
  <li>각 항목 앞에 ◦ 표시</li>
</ul>

<ul class="none-list">
  <li>목록 기호 없이 표시</li>
  <li>디자인에 따라 목록 기호 제거 가능</li>
</ul>
목록 스타일 변경 예시

disc (기본값) : ●
circle : ○
square : ■
none : 기호 없이 목록 표시
3. 중첩된 목록
리스트 안에 또 다른 리스트를 포함하여 중첩된 구조를 만들 수 있다.
게임에서 메뉴 트리나 퀘스트 목표 리스트를 만들 때 유용하다.

<ul>
  <li>
    무기 종류
    <ul>
      <li>검</li>
      <li>활</li>
      <li>마법 지팡이</li>
    </ul>
  </li>
  <li>
    방어구
    <ul>
      <li>갑옷</li>
      <li>방패</li>
    </ul>
  </li>
</ul>
위 코드를 실행하면 다음과 같이 중첩된 목록이 출력된다.

무기 종류
검
활
마법 지팡이
방어구
갑옷
방패
4. 순서 없는 목록을 게임 UI에서 활용하기
순서 없는 목록은 게임의 UI 요소를 만들 때 유용하다.
특히, 인벤토리 목록이나 퀘스트 목록을 표시할 때 활용할 수 있다.

<h3>인벤토리</h3>
<ul>
  <li>강철 검</li>
  <li>체력 회복 물약</li>
  <li>마법 두루마리</li>
</ul>
이런 방식으로 게임 내 아이템을 쉽게 목록 형태로 표시할 수 있다.

5. CSS를 이용한 스타일링
기본 목록 스타일을 그대로 사용하기보다는, 게임 UI에 맞게 디자인하는 것이 중요하다.
CSS를 활용하면 목록 항목을 아이콘 형태로 변경하거나, 특정 스타일을 적용할 수 있다.

<style>
  .custom-list {
    list-style: none;
    padding: 0;
  }
  .custom-list li {
    background: url("star-icon.png") no-repeat left center;
    padding-left: 30px;
    line-height: 24px;
  }
</style>

<ul class="custom-list">
  <li>전설의 검</li>
  <li>마법 방패</li>
  <li>체력 회복 물약</li>
</ul>
위 코드는 각 목록 항목 앞에 이미지를 삽입하여, 게임의 UI에서 더욱 직관적인 아이템 리스트를 만들 수 있도록 한다.

학습자의 사고를 돕기 위한 질문
순서 없는 목록(<ul>)과 순서 있는 목록(<ol>)의 차이는 무엇인가?

각 목록의 용도와 사용 사례를 고려해보라.
HTML 문서에서 <ul> 태그를 사용하면 어떤 시각적 효과가 나타나는가?

기본 스타일과 브라우저 렌더링 방식을 떠올려보라.
실습 문제
문제 1: 순서 없는 목록 만들기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<ul> 태그를 사용하여 "좋아하는 음식 목록"을 작성한다.
<li> 태그를 사용하여 3개 이상의 항목을 추가한다.
목록이 올바르게 표시되는지 확인한다.
5.2. 순서 있는 목록 (<ol>, <li>)
순서 있는 목록(Ordered List)은 <ol> 태그와 <li> 태그를 사용하여 생성된다.
목록의 순서가 중요한 경우에 사용되며, 기본적으로 숫자(1, 2, 3...)가 목록 앞에 자동으로 부여된다.

1. 기본적인 순서 있는 목록
순서가 중요한 게임 플레이 단계나 퀘스트 진행 순서 등을 표시할 때 유용하다.

<ol>
  <li>게임 시작</li>
  <li>캐릭터 선택</li>
  <li>튜토리얼 진행</li>
  <li>첫 번째 퀘스트 완료</li>
</ol>
출력 결과:

게임 시작
캐릭터 선택
튜토리얼 진행
첫 번째 퀘스트 완료
자동으로 숫자가 붙으며, 순서가 중요한 경우 활용할 수 있다.

2. 목록 스타일 변경
HTML에서 <ol> 태그의 type 속성을 사용하면 다양한 방식으로 목록 번호를 변경할 수 있다.

<ol type="A">
  <li>전사</li>
  <li>마법사</li>
  <li>도적</li>
</ol>

<ol type="a">
  <li>소드 마스터</li>
  <li>파이어 메이지</li>
  <li>어쌔신</li>
</ol>

<ol type="I">
  <li>1단계 보스</li>
  <li>2단계 보스</li>
  <li>최종 보스</li>
</ol>

<ol type="i">
  <li>레벨 1</li>
  <li>레벨 2</li>
  <li>레벨 3</li>
</ol>
출력 결과

type="A" → A, B, C, ...
type="a" → a, b, c, ...
type="I" → I, II, III, ...
type="i" → i, ii, iii, ...
이러한 스타일은 순위 시스템이나 퀘스트 단계를 표현할 때 유용하다.

3. 시작 숫자 변경
게임에서 퀘스트 진행도나 점수 랭킹을 표시할 때 특정 숫자에서 시작해야 하는 경우가 있다.
이때, start 속성을 사용하면 목록의 시작 숫자를 조정할 수 있다.

<ol start="5">
  <li>다섯 번째 퀘스트</li>
  <li>여섯 번째 퀘스트</li>
  <li>일곱 번째 퀘스트</li>
</ol>
출력 결과 5. 다섯 번째 퀘스트 6. 여섯 번째 퀘스트 7. 일곱 번째 퀘스트

start="5"을 사용하여 목록의 시작값을 5로 설정하였다.

4. 중첩된 순서 있는 목록
순서 있는 목록은 중첩하여 사용할 수도 있다.
예를 들어, 게임의 튜토리얼 단계를 세분화하여 표시할 때 유용하다.

<ol>
  <li>
    기본 조작 익히기
    <ol>
      <li>이동</li>
      <li>점프</li>
      <li>공격</li>
    </ol>
  </li>
  <li>
    전투 튜토리얼
    <ol>
      <li>적 조준</li>
      <li>콤보 사용</li>
      <li>특수 스킬 활용</li>
    </ol>
  </li>
</ol>
출력 결과

기본 조작 익히기
이동
점프
공격
전투 튜토리얼
적 조준
콤보 사용
특수 스킬 활용
이처럼 게임 내에서 단계별 학습 시스템을 만들 때 적절하게 활용할 수 있다.

5. CSS를 활용한 순서 있는 목록 스타일링
게임의 UI에 맞춰 순서 있는 목록을 커스터마이징할 수도 있다.
CSS를 사용하여 번호 대신 아이콘을 활용하는 것도 가능하다.

<style>
  .custom-ol {
    counter-reset: custom-counter;
    list-style: none;
    padding: 0;
  }
  .custom-ol li {
    counter-increment: custom-counter;
    position: relative;
    padding-left: 30px;
  }
  .custom-ol li::before {
    content: counter(custom-counter) ". ";
    font-weight: bold;
    color: #ff6600;
    position: absolute;
    left: 0;
  }
</style>

<ol class="custom-ol">
  <li>전설 아이템 획득</li>
  <li>최종 보스 처치</li>
  <li>엔딩 보기</li>
</ol>
위 코드를 적용하면 목록 앞의 숫자가 게임 스타일에 맞게 강조된다.

학습자의 사고를 돕기 위한 질문
순서 있는 목록(<ol>)을 사용하면 어떤 장점이 있는가?

단계적인 정보를 표시할 때의 효과를 고려해보라.
HTML 문서에서 <ol> 태그의 기본 번호 매김 방식을 변경하는 방법은 무엇인가?

type 속성과 start 속성을 떠올려보라.
실습 문제
문제 1: 순서 있는 목록 만들기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<ol> 태그를 사용하여 "아침 루틴" 목록을 작성한다.
<li> 태그를 사용하여 루틴을 5단계 이상 작성한다.
목록이 1부터 시작하도록 설정한다.
5.3. 정의 목록 (<dl>, <dt>, <dd>)
정의 목록(Definition List)은 특정 용어와 그에 대한 설명을 함께 표시하는 데 사용된다.
보통 사전식 표현이나 용어 설명, 게임의 스킬 설명 등에서 활용할 수 있다.

HTML에서 정의 목록을 만들기 위해 다음과 같은 태그를 사용한다.

<dl>: 정의 목록을 감싸는 태그
<dt>: 용어(term)를 정의하는 태그
<dd>: 용어의 설명을 작성하는 태그
1. 기본적인 정의 목록
게임 내 스킬 설명을 정의 목록으로 나타낼 수 있다.

<dl>
  <dt>파이어볼</dt>
  <dd>불덩이를 발사하여 적에게 50의 화염 피해를 준다.</dd>

  <dt>힐링</dt>
  <dd>자신 또는 아군의 체력을 30 회복시킨다.</dd>

  <dt>스텔스</dt>
  <dd>10초 동안 적에게 보이지 않게 된다.</dd>
</dl>
출력 결과

파이어볼: 불덩이를 발사하여 적에게 50의 화염 피해를 준다.
힐링: 자신 또는 아군의 체력을 30 회복시킨다.
스텔스: 10초 동안 적에게 보이지 않게 된다.
이와 같이 게임 내에서 아이템 설명이나 스킬 효과를 설명할 때 정의 목록이 유용하다.

2. 여러 줄에 걸친 설명
경우에 따라 설명이 길어질 수도 있다. 이때, <dd> 태그 안에 여러 개의 문장을 넣을 수 있다.

<dl>
  <dt>포션</dt>
  <dd>체력을 50 회복하는 아이템이다. 전투 중에도 사용할 수 있다.</dd>

  <dt>마나 포션</dt>
  <dd>
    사용 시 즉시 마나를 30 회복한다.<br />
    재사용 대기시간: 10초
  </dd>
</dl>
출력 결과

포션: 체력을 50 회복하는 아이템이다. 전투 중에도 사용할 수 있다.
마나 포션:
사용 시 즉시 마나를 30 회복한다.
재사용 대기시간: 10초
줄바꿈을 위해 <br> 태그를 사용할 수도 있다.

3. 중첩된 정의 목록
정의 목록은 중첩하여 사용할 수도 있다.
예를 들어 RPG 게임의 직업별 스킬 목록을 표현할 때 적절하다.

<dl>
  <dt>전사</dt>
  <dd>
    <dl>
      <dt>방패 막기</dt>
      <dd>적의 공격을 50% 확률로 막아낸다.</dd>

      <dt>강타</dt>
      <dd>대검을 사용하여 적에게 강력한 피해를 입힌다.</dd>
    </dl>
  </dd>

  <dt>마법사</dt>
  <dd>
    <dl>
      <dt>파이어볼</dt>
      <dd>불덩이를 발사하여 적에게 화염 피해를 입힌다.</dd>

      <dt>아이스 스톰</dt>
      <dd>주변을 얼려 적을 느리게 만든다.</dd>
    </dl>
  </dd>
</dl>
출력 결과

전사

방패 막기: 적의 공격을 50% 확률로 막아낸다.
강타: 대검을 사용하여 적에게 강력한 피해를 입힌다.
마법사

파이어볼: 불덩이를 발사하여 적에게 화염 피해를 입힌다.
아이스 스톰: 주변을 얼려 적을 느리게 만든다.
이처럼 게임 내 직업 시스템, 아이템 효과, 퀘스트 정보 등을 체계적으로 정리할 때 중첩된 정의 목록을 활용할 수 있다.

4. CSS를 활용한 정의 목록 스타일링
기본적인 정의 목록은 스타일이 단순하지만, CSS를 활용하면 게임 UI에 맞게 스타일을 조정할 수 있다.

<style>
  dl {
    font-family: Arial, sans-serif;
    width: 300px;
    background: #222;
    color: #fff;
    padding: 10px;
    border-radius: 10px;
  }
  dt {
    font-weight: bold;
    color: #ffcc00;
    margin-top: 10px;
  }
  dd {
    margin-left: 15px;
    font-size: 14px;
  }
</style>

<dl>
  <dt>전설의 검</dt>
  <dd>공격력 +50, 치명타 확률 +10%</dd>

  <dt>신성한 방패</dt>
  <dd>방어력 +30, 모든 속성 저항 +5%</dd>
</dl>
스타일 적용 후 출력 결과:

배경색을 어둡게 설정하여 게임 아이템 툴팁 스타일을 재현했다.
<dt> 태그(아이템 이름)는 금색(#ffcc00) 으로 강조하였다.
<dd> 태그(설명)는 글씨 크기를 줄이고 들여쓰기 하여 가독성을 높였다.
이와 같이 게임 인벤토리에서 아이템 설명을 제공할 때 유용하게 활용할 수 있다.

학습자의 사고를 돕기 위한 질문
정의 목록(<dl>)을 사용할 때 적절한 예시는 무엇인가?

사전, 용어집, 설명 목록의 활용 사례를 떠올려보라.
정의 목록(<dl>, <dt>, <dd>)이 <ul> 또는 <ol>과 다른 점은 무엇인가?

데이터 표현 방식의 차이를 고려해보라.
실습 문제
문제 1: 정의 목록 만들기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<dl> 태그를 사용하여 "웹 개발 용어집"을 작성한다.
<dt> 태그를 사용하여 용어(예: HTML, CSS, JavaScript)를 정의한다.
<dd> 태그를 사용하여 해당 용어의 설명을 추가한다.
5.4. 리스트 중첩 구조
HTML에서 목록 태그(<ul>, <ol>, <dl>)는 서로 중첩하여 사용할 수 있다.
이를 통해 게임 내 메뉴, 퀘스트 진행 단계, 캐릭터 스킬 트리 같은 계층적 구조를 표현할 수 있다.

1. 중첩된 순서 없는 목록 (<ul>)
중첩된 <ul> 목록은 게임의 UI에서 메뉴를 구성할 때 자주 사용된다.
예를 들어, RPG 게임의 인벤토리 카테고리를 구현할 수 있다.

<ul>
  <li>
    장비
    <ul>
      <li>무기</li>
      <li>방어구</li>
      <li>장신구</li>
    </ul>
  </li>
  <li>
    소모품
    <ul>
      <li>포션</li>
      <li>스크롤</li>
    </ul>
  </li>
  <li>퀘스트 아이템</li>
</ul>
출력 결과

장비
무기
방어구
장신구
소모품
포션
스크롤
퀘스트 아이템
이렇게 중첩된 목록을 활용하면 계층적인 구조의 아이템 시스템을 쉽게 표현할 수 있다.

2. 중첩된 순서 있는 목록 (<ol>)
순서 있는 목록(<ol>)을 중첩하면 게임 내 퀘스트 진행 과정을 표시할 수 있다.

<ol>
  <li>
    퀘스트 수락
    <ol>
      <li>NPC와 대화</li>
      <li>목표 확인</li>
    </ol>
  </li>
  <li>
    목표 수행
    <ol>
      <li>몬스터 처치</li>
      <li>아이템 수집</li>
    </ol>
  </li>
  <li>
    퀘스트 완료
    <ol>
      <li>NPC에게 보고</li>
      <li>보상 수령</li>
    </ol>
  </li>
</ol>
출력 결과

퀘스트 수락
NPC와 대화
목표 확인
목표 수행
몬스터 처치
아이템 수집
퀘스트 완료
NPC에게 보고
보상 수령
이처럼 퀘스트 수행 과정을 단계별로 표현할 때 유용하다.

3. 순서 없는 목록과 순서 있는 목록의 조합
게임 내 스킬 트리를 표현할 때, 주 스킬(메인 카테고리) 은 순서 없는 목록(<ul>)으로,
세부 스킬의 습득 순서는 순서 있는 목록(<ol>)으로 구성하면 좋다.

<ul>
  <li>
    마법사
    <ol>
      <li>파이어볼</li>
      <li>파이어 스톰</li>
      <li>메테오</li>
    </ol>
  </li>
  <li>
    전사
    <ol>
      <li>강타</li>
      <li>대지 가르기</li>
      <li>광폭화</li>
    </ol>
  </li>
</ul>
출력 결과

마법사
파이어볼
파이어 스톰
메테오
전사
강타
대지 가르기
광폭화
이런 방식으로 스킬 트리, 업그레이드 순서 등을 표현할 수 있다.

4. 정의 목록을 활용한 중첩 구조
정의 목록(<dl>)을 중첩하면 게임 속 캐릭터 설명을 정리하는 데 유용하다.

<dl>
  <dt>마법사</dt>
  <dd>
    <dl>
      <dt>특징</dt>
      <dd>원거리 마법 공격을 사용한다.</dd>
      <dt>주요 스킬</dt>
      <dd>파이어볼, 아이스 스톰</dd>
    </dl>
  </dd>

  <dt>전사</dt>
  <dd>
    <dl>
      <dt>특징</dt>
      <dd>근접 공격과 높은 방어력을 갖춘 클래스.</dd>
      <dt>주요 스킬</dt>
      <dd>강타, 방패 막기</dd>
    </dl>
  </dd>
</dl>
출력 결과

마법사
특징: 원거리 마법 공격을 사용한다.
주요 스킬: 파이어볼, 아이스 스톰
전사
특징: 근접 공격과 높은 방어력을 갖춘 클래스.
주요 스킬: 강타, 방패 막기
이처럼 정의 목록을 사용하면 캐릭터 설명, 아이템 효과 정리 등을 보다 직관적으로 정리할 수 있다.

5. CSS를 활용한 중첩 목록 스타일링
HTML의 기본 목록 스타일은 단순하기 때문에, CSS를 적용하여 게임 UI와 어울리는 디자인을 만들 수 있다.

<style>
  ul {
    list-style-type: none;
    padding-left: 15px;
  }
  ul li {
    background: #333;
    color: white;
    padding: 5px;
    margin: 5px 0;
    border-radius: 5px;
  }
  ol {
    padding-left: 20px;
    color: yellow;
  }
</style>

<ul>
  <li>
    전사
    <ol>
      <li>강타</li>
      <li>방패 막기</li>
    </ol>
  </li>
  <li>
    마법사
    <ol>
      <li>파이어볼</li>
      <li>아이스 스톰</li>
    </ol>
  </li>
</ul>
스타일 적용 후 출력 결과

전사
강타
방패 막기
마법사
파이어볼
아이스 스톰
위 스타일을 적용하면 배경색, 테두리, 글자색을 변경하여 게임 UI처럼 표현할 수 있다.

학습자의 사고를 돕기 위한 질문
HTML에서 중첩 리스트를 사용할 때 <ul>과 <ol>을 섞어서 사용할 수 있는가?

서로 다른 목록 유형을 함께 사용할 때의 유용성을 생각해보라.
중첩 리스트를 사용할 때 가독성을 높이기 위한 방법은 무엇인가?

들여쓰기와 계층 구조를 고려해보라.
실습 문제
문제 1: 중첩 리스트 만들기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<ul> 태그를 사용하여 "프로그래밍 언어 목록"을 작성한다.
각 항목에 대해 <ol> 태그를 사용하여 "대표적인 프레임워크"를 포함한다.
적어도 2개 이상의 프로그래밍 언어와 각각의 프레임워크를 작성한다.
6. 테이블 구성
6.1. 테이블 태그의 기본 구조
HTML 테이블은 데이터를 행(row)과 열(column)의 구조로 배치할 때 사용한다.
웹 페이지에서 순위표, 리더보드, 게임 아이템 목록 같은 데이터를 정리하는 데 유용하다.

1. 테이블의 기본 구조
HTML 테이블은 <table> 태그로 정의되며, 다음과 같은 기본 요소를 포함한다.

<tr>: 행(Row) 을 생성하는 태그
<th>: 제목(Header) 셀을 정의하는 태그
<td>: 데이터(Data) 셀을 정의하는 태그
다음 예제는 RPG 게임의 캐릭터 정보 테이블을 나타낸다.

<table border="1">
  <tr>
    <th>이름</th>
    <th>직업</th>
    <th>레벨</th>
  </tr>
  <tr>
    <td>아르테미스</td>
    <td>궁수</td>
    <td>45</td>
  </tr>
  <tr>
    <td>타이탄</td>
    <td>전사</td>
    <td>50</td>
  </tr>
</table>
출력 결과

이름	직업	레벨
아르테미스	궁수	45
타이탄	전사	50
위와 같이 테이블을 활용하면 게임 내 캐릭터 목록, 인벤토리, 리더보드 등을 구성할 수 있다.

2. border 속성
border 속성을 사용하면 테이블에 테두리를 추가할 수 있다.
기본적으로 HTML5에서는 border 속성을 CSS에서 설정하는 것이 권장된다.

<style>
  table {
    border-collapse: collapse;
    width: 50%;
  }
  th,
  td {
    border: 1px solid black;
    padding: 8px;
    text-align: center;
  }
</style>

<table>
  <tr>
    <th>아이템</th>
    <th>종류</th>
    <th>공격력</th>
  </tr>
  <tr>
    <td>불의 검</td>
    <td>무기</td>
    <td>50</td>
  </tr>
  <tr>
    <td>수호자의 방패</td>
    <td>방어구</td>
    <td>10</td>
  </tr>
</table>
출력 결과

아이템	종류	공격력
불의 검	무기	50
수호자의 방패	방어구	10
위 테이블은 게임의 인벤토리 UI에서 무기 및 방어구 정보를 정리할 때 유용하다.

3. 테이블의 행과 열
테이블은 여러 개의 행과 열을 포함할 수 있다.
각 행(<tr>) 내부에 제목 셀(<th>) 또는 데이터 셀(<td>) 을 배치한다.

아래 예제는 게임 리더보드(순위표) 를 나타낸다.

<table>
  <tr>
    <th>순위</th>
    <th>닉네임</th>
    <th>점수</th>
  </tr>
  <tr>
    <td>1</td>
    <td>DarkKnight</td>
    <td>1500</td>
  </tr>
  <tr>
    <td>2</td>
    <td>FireMage</td>
    <td>1400</td>
  </tr>
  <tr>
    <td>3</td>
    <td>StormBringer</td>
    <td>1300</td>
  </tr>
</table>
출력 결과

순위	닉네임	점수
1	DarkKnight	1500
2	FireMage	1400
3	StormBringer	1300
이러한 리더보드 테이블을 활용하면 웹에서 게임의 순위 시스템을 정리할 수 있다.

4. 테이블과 CSS 스타일링
테이블은 CSS를 활용하여 더욱 깔끔하게 디자인할 수 있다.

<style>
  table {
    border-collapse: collapse;
    width: 80%;
    margin: 20px 0;
  }
  th,
  td {
    border: 1px solid #ddd;
    padding: 10px;
    text-align: center;
  }
  th {
    background-color: #4caf50;
    color: white;
  }
  tr:nth-child(even) {
    background-color: #f2f2f2;
  }
</style>

<table>
  <tr>
    <th>스킬명</th>
    <th>타입</th>
    <th>마나 소모량</th>
  </tr>
  <tr>
    <td>파이어볼</td>
    <td>마법 공격</td>
    <td>20</td>
  </tr>
  <tr>
    <td>힐링</td>
    <td>회복</td>
    <td>15</td>
  </tr>
</table>
출력 결과

스킬명	타입	마나 소모량
파이어볼	마법 공격	20
힐링	회복	15
CSS를 적용하면 가독성이 뛰어난 게임 UI 테이블을 만들 수 있다.

학습자의 사고를 돕기 위한 질문
HTML 테이블을 사용할 때 <tr>, <th>, <td> 태그의 역할은 무엇인가?

테이블 행과 데이터 셀의 구조를 떠올려보라.
테이블을 활용할 때 CSS로 스타일을 조정할 수 있는 요소에는 어떤 것들이 있는가?

테두리, 배경색, 정렬 방식을 고려해보라.
실습 문제
문제 1: 기본 테이블 만들기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<table> 태그를 사용하여 학생들의 성적표를 만든다.
<tr> 태그를 사용하여 3개 이상의 행을 추가한다.
<th> 태그를 사용하여 "이름", "수학", "영어", "과학" 등의 열 제목을 만든다.
<td> 태그를 사용하여 각 학생의 점수를 입력한다.
6.2. 테이블 속성 활용
HTML 테이블은 여러 속성을 활용하여 다양한 형태로 커스터마이징할 수 있다.
특히 colspan과 rowspan 속성을 이용하면 셀 병합이 가능하며,
여백과 테두리를 조정하는 cellpadding, cellspacing, border 속성도 자주 사용된다.
이러한 기능들은 게임 UI에서 캐릭터 능력치, 아이템 목록, 리더보드 등을 효과적으로 표현하는 데 유용하다.

1. colspan을 활용한 셀 병합 (가로 병합)
colspan 속성은 가로 방향으로 여러 셀을 하나로 병합할 때 사용된다.
예를 들어, RPG 게임의 퀘스트 보상 목록을 표시할 때 사용할 수 있다.

<table border="1">
  <tr>
    <th colspan="3">퀘스트 보상</th>
  </tr>
  <tr>
    <th>아이템</th>
    <th>종류</th>
    <th>가치</th>
  </tr>
  <tr>
    <td>에픽 검</td>
    <td>무기</td>
    <td>1000 골드</td>
  </tr>
  <tr>
    <td>힐링 포션</td>
    <td>소모품</td>
    <td>50 골드</td>
  </tr>
</table>
출력 결과

퀘스트 보상
아이템
에픽 검
힐링 포션
첫 번째 행의 <th colspan="3">퀘스트 보상</th> 설정으로 가로 3칸을 병합했다.
이를 활용하면 게임 보상 시스템을 정리하는 UI에 적합하다.
2. rowspan을 활용한 셀 병합 (세로 병합)
rowspan 속성은 세로 방향으로 여러 행을 하나의 셀로 병합할 때 사용된다.
예를 들어, 게임 내 던전 보상 아이템 목록을 정리할 때 유용하다.

<table border="1">
  <tr>
    <th>던전</th>
    <th>아이템</th>
    <th>등급</th>
  </tr>
  <tr>
    <td rowspan="2">고블린 동굴</td>
    <td>고블린 검</td>
    <td>일반</td>
  </tr>
  <tr>
    <td>고블린 방패</td>
    <td>희귀</td>
  </tr>
  <tr>
    <td rowspan="3">드래곤 둥지</td>
    <td>드래곤 창</td>
    <td>전설</td>
  </tr>
  <tr>
    <td>드래곤 갑옷</td>
    <td>영웅</td>
  </tr>
  <tr>
    <td>불꽃 반지</td>
    <td>희귀</td>
  </tr>
</table>
출력 결과

던전	아이템	등급
고블린 동굴	고블린 검	일반
고블린 방패	희귀
드래곤 둥지	드래곤 창	전설
드래곤 갑옷	영웅
불꽃 반지	희귀
<td rowspan="2">고블린 동굴</td> 설정으로 두 개의 행을 병합했다.
<td rowspan="3">드래곤 둥지</td> 설정으로 세 개의 행을 병합했다.
이를 활용하면 던전별 획득 가능 아이템 목록을 효과적으로 정리할 수 있다.
3. cellpadding과 cellspacing 속성
cellpadding: 셀 안의 여백을 조절하는 속성
cellspacing: 셀 간의 간격을 조절하는 속성
다음 예제는 게임 내 장비 상점 UI에서 cellpadding과 cellspacing을 조절한 테이블을 보여준다.

<table border="1" cellpadding="10" cellspacing="5">
  <tr>
    <th>아이템</th>
    <th>가격</th>
    <th>설명</th>
  </tr>
  <tr>
    <td>마법의 지팡이</td>
    <td>1500 골드</td>
    <td>마법 공격력 +10</td>
  </tr>
  <tr>
    <td>전사의 검</td>
    <td>1200 골드</td>
    <td>물리 공격력 +15</td>
  </tr>
</table>
출력 결과

아이템	가격	설명
마법의 지팡이	1500 골드	마법 공격력 +10
전사의 검	1200 골드	물리 공격력 +15
cellpadding="10"을 사용하여 셀 내부 여백을 넉넉하게 확보했다.
cellspacing="5"을 사용하여 셀 간 간격을 추가했다.
이를 활용하면 게임 아이템 상점 UI를 더 깔끔하게 만들 수 있다.
4. border-collapse 속성
CSS의 border-collapse 속성은 셀 테두리를 하나로 합치는 기능을 한다.
이를 활용하면 테이블을 더욱 정돈된 형태로 만들 수 있다.

<style>
  table {
    border-collapse: collapse;
    width: 60%;
  }
  th,
  td {
    border: 1px solid black;
    padding: 10px;
    text-align: center;
  }
</style>

<table>
  <tr>
    <th>아이템</th>
    <th>등급</th>
    <th>효과</th>
  </tr>
  <tr>
    <td>엘릭서</td>
    <td>전설</td>
    <td>체력 및 마나 완전 회복</td>
  </tr>
  <tr>
    <td>힘의 포션</td>
    <td>희귀</td>
    <td>공격력 10% 증가</td>
  </tr>
</table>
출력 결과

아이템	등급	효과
엘릭서	전설	체력 및 마나 완전 회복
힘의 포션	희귀	공격력 10% 증가
border-collapse: collapse; 속성을 추가하여 셀 테두리가 하나로 합쳐져 깔끔해졌다.
text-align: center;를 사용해 내용이 중앙 정렬되었다.
이러한 설정은 게임 내 아이템 목록 UI에서 유용하다.
학습자의 사고를 돕기 위한 질문
테이블에서 colspan과 rowspan 속성은 각각 어떤 역할을 하는가?

셀을 병합할 때의 활용 사례를 고려해보라.
border, cellpadding, cellspacing 속성을 사용할 때 시각적으로 어떤 효과가 나타나는가?

테이블의 테두리, 셀 내부 여백을 비교해보라.
실습 문제
문제 1: 셀 병합이 포함된 테이블 만들기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<table> 태그를 사용하여 시간표를 만든다.
colspan 속성을 사용하여 "점심시간"이 한 행 전체를 차지하도록 설정한다.
rowspan 속성을 사용하여 특정 과목이 2교시에 걸쳐 표시되도록 설정한다.
7. 폼 요소와 사용자 입력 태그
7.1. <form> 태그의 역할
HTML에서 <form> 태그는 사용자가 입력한 데이터를 서버로 전송하기 위한 컨테이너 역할을 한다.
폼을 활용하면 회원가입, 로그인, 게임 내 점수 제출, 캐릭터 정보 입력 등의 기능을 구현할 수 있다.
예를 들어, 게임 내 플레이어 프로필을 설정하는 폼을 만들 수도 있다.

1. <form> 태그의 기본 구조
<form> 태그는 내부에 다양한 입력 요소 (<input>, <textarea>, <select> 등) 를 포함하며,
action 속성을 통해 입력된 데이터를 전송할 서버 주소를 지정한다.
method 속성을 사용하여 전송 방식을 결정할 수 있다.

<form action="/submit-profile" method="post">
  <label for="username">플레이어 이름:</label>
  <input type="text" id="username" name="username" required />

  <label for="email">이메일:</label>
  <input type="email" id="email" name="email" required />

  <button type="submit">제출</button>
</form>
설명

action="/submit-profile" → 데이터를 서버의 /submit-profile로 전송
method="post" → 입력한 정보를 숨기고 서버로 전달 (GET 방식과 차이 있음)
required 속성 추가 → 필수 입력 필드
게임 개발에서 활용 예시

게임 프로필 설정: 플레이어가 닉네임을 설정하고, 이메일을 등록하는 UI.
게임 점수 제출: 최고 점수를 서버로 전송하여 랭킹 시스템 구축.
2. method 속성: GET vs POST
method 속성은 데이터를 전송하는 방식을 결정한다.
주로 GET과 POST가 사용되며, 사용 목적에 따라 다르게 선택해야 한다.

전송 방식	특징	사용 예
GET	URL에 데이터가 포함됨	검색, 필터 기능
POST	데이터가 URL에 노출되지 않음	로그인, 회원가입
예제: GET 방식으로 플레이어 검색하기

<form action="/search" method="get">
  <label for="player">플레이어 검색:</label>
  <input type="text" id="player" name="player" />
  <button type="submit">검색</button>
</form>
GET 방식은 데이터를 URL로 보낸다.
예를 들어 player=John을 입력하면 /search?player=John 형태로 서버에 요청한다.

예제: POST 방식으로 회원가입하기

<form action="/register" method="post">
  <label for="username">아이디:</label>
  <input type="text" id="username" name="username" />

  <label for="password">비밀번호:</label>
  <input type="password" id="password" name="password" />

  <button type="submit">가입하기</button>
</form>
POST 방식은 입력값을 URL이 아닌 요청 본문(body)에 포함시킨다.
따라서 보안이 중요한 회원가입, 로그인, 결제 등의 기능에서 사용된다.

3. <form> 태그의 주요 속성
속성	설명	예제
action	데이터를 보낼 서버 URL	action="/submit"
method	데이터 전송 방식 (GET, POST)	method="post"
target	전송 결과를 어디에 표시할지	target="_blank" (새 창)
enctype	파일 업로드 시 필요	enctype="multipart/form-data"
예제: 파일 업로드를 위한 enctype 속성

<form action="/upload" method="post" enctype="multipart/form-data">
  <label for="avatar">프로필 사진 업로드:</label>
  <input type="file" id="avatar" name="avatar" />
  <button type="submit">업로드</button>
</form>
enctype="multipart/form-data"를 지정해야 이미지, 동영상 업로드 가능.
게임에서 프로필 사진 설정, 스크린샷 업로드 기능에 적용 가능.
4. <form> 태그와 JavaScript 활용
게임 내 실시간 입력 검증이나 AJAX 요청을 통한 서버 통신을 할 때,
JavaScript와 함께 <form>을 사용할 수 있다.

예제: JavaScript를 사용한 유효성 검사

<form id="gameForm">
  <label for="nickname">닉네임:</label>
  <input type="text" id="nickname" name="nickname" />
  <button type="submit">제출</button>
</form>

<script>
  document
    .getElementById("gameForm")
    .addEventListener("submit", function (event) {
      let nickname = document.getElementById("nickname").value;
      if (nickname.length < 3) {
        alert("닉네임은 최소 3글자 이상이어야 합니다.");
        event.preventDefault(); // 폼 제출 방지
      }
    });
</script>
닉네임 길이 검증: 3글자 미만이면 제출되지 않도록 설정.
게임 내 닉네임 입력 시 필터링 적용 가능.
학습자의 사고를 돕기 위한 질문
HTML에서 <form> 태그의 기본 역할은 무엇인가?

사용자 입력 데이터를 서버로 전송하는 과정을 떠올려보라.
폼 데이터를 전송할 때 GET과 POST 방식의 차이점은 무엇인가?

데이터 보안과 전송 방식의 차이를 고려해보라.
7.2. 다양한 <input> 타입
HTML의 <input> 태그는 사용자로부터 데이터를 입력받는 핵심 요소이다.
각각의 type 속성값에 따라 다양한 입력 방식을 제공하며,
게임 개발에서도 유저 설정, 캐릭터 생성, 점수 입력 등 다양한 상황에서 활용된다.

1. 텍스트 입력 (type="text")
가장 기본적인 입력 필드로, 한 줄의 문자열을 입력받을 때 사용한다.

<label for="username">플레이어 이름:</label>
<input type="text" id="username" name="username" placeholder="닉네임 입력" />
속성

placeholder="닉네임 입력" → 입력란에 힌트 제공
maxlength="12" → 입력 길이를 제한할 수도 있음
활용 예시

게임 내 닉네임 설정: 사용자가 캐릭터 닉네임을 입력할 때 사용.
2. 비밀번호 입력 (type="password")
비밀번호 입력을 위한 필드로, 입력값이 숨겨진 상태(●●●)로 표시된다.

<label for="password">비밀번호:</label>
<input
  type="password"
  id="password"
  name="password"
  placeholder="비밀번호 입력"
/>
활용 예시

로그인 및 회원가입 시스템: 유저가 게임에 로그인할 때 사용.
3. 체크박스 (type="checkbox")
하나 이상의 옵션을 선택할 수 있도록 하는 입력 방식이다.

<label>
  <input type="checkbox" name="sound" checked />
  배경 음악 활성화
</label>
속성

checked → 기본적으로 선택된 상태로 설정
활용 예시

게임 옵션 설정: 배경 음악, 효과음 활성화 여부를 설정할 때 유용.
4. 라디오 버튼 (type="radio")
서로 다른 여러 옵션 중 하나만 선택하도록 강제할 때 사용한다.

<label>
  <input type="radio" name="difficulty" value="easy" checked />
  쉬움
</label>
<label>
  <input type="radio" name="difficulty" value="hard" />
  어려움
</label>
속성

같은 name="difficulty" 값을 가지면 한 개만 선택 가능.
활용 예시

게임 난이도 선택: 쉬움, 보통, 어려움 중 하나를 선택할 때 유용.
5. 숫자 입력 (type="number")
숫자만 입력할 수 있도록 제한하는 입력 필드이다.

<label for="age">나이 입력:</label>
<input type="number" id="age" name="age" min="1" max="100" />
속성

min="1", max="100" → 입력 가능 범위 지정 가능
활용 예시

게임 내 캐릭터 나이 설정: 플레이어가 캐릭터 생성 시 나이를 입력할 때 사용.
6. 범위 선택 (type="range")
슬라이더를 통해 값을 조정할 수 있도록 한다.

<label for="volume">배경음악 볼륨:</label>
<input type="range" id="volume" name="volume" min="0" max="100" value="50" />
활용 예시

게임 내 사운드 볼륨 조절: 슬라이더를 이용해 배경음악 볼륨을 조정할 때 사용.
7. 날짜 입력 (type="date")
달력 UI를 통해 날짜를 선택할 수 있는 입력 필드이다.

<label for="birthdate">생년월일:</label>
<input type="date" id="birthdate" name="birthdate" />
활용 예시

게임 내 출생 연도 선택: 유저가 캐릭터의 생년월일을 설정할 때 유용.
8. 파일 업로드 (type="file")
유저가 이미지, 문서, 영상 파일 등을 업로드할 수 있도록 한다.

<label for="avatar">프로필 사진 업로드:</label>
<input type="file" id="avatar" name="avatar" />
활용 예시

게임 프로필 사진 업로드: 유저가 자신의 캐릭터 아바타 이미지를 설정할 때 사용.
9. 이메일 입력 (type="email")
이메일 형식의 입력값을 받을 때 사용하며, 자동으로 유효성 검사를 적용한다.

<label for="email">이메일:</label>
<input type="email" id="email" name="email" required />
활용 예시

회원가입 및 이메일 인증: 게임 계정의 이메일 정보를 입력받을 때 사용.
10. 색상 선택 (type="color")
컬러 피커를 제공하여 사용자가 원하는 색상을 선택할 수 있도록 한다.

<label for="color">캐릭터 색상 선택:</label>
<input type="color" id="color" name="color" />
활용 예시

캐릭터 커스터마이징: 플레이어가 캐릭터의 머리 색상이나 옷 색상을 설정할 때 사용.
학습자의 사고를 돕기 위한 질문
HTML <input> 태그의 다양한 타입에는 어떤 것들이 있는가?

텍스트 입력, 체크박스, 라디오 버튼 등을 떠올려보라.
사용자가 올바른 데이터를 입력하도록 도와주는 HTML 속성은 무엇인가?

placeholder, required, maxlength 속성을 고려해보라.
실습 문제
문제 1: 다양한 입력 필드 포함한 폼 만들기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<input> 태그를 사용하여 다음 항목을 포함하는 폼을 만든다.
사용자 이름 입력 (텍스트 필드)
비밀번호 입력 (비밀번호 필드)
생년월일 선택 (날짜 필드)
성별 선택 (라디오 버튼)
관심 분야 선택 (체크박스)
제출 버튼
7.3. 버튼과 폼 제출
HTML에서 폼(form) 제출을 위한 버튼은 다양한 방식으로 구현할 수 있다.
버튼은 사용자의 입력을 완료하고 폼을 서버로 전송하는 역할을 하며,
기본 <button> 태그 또는 <input> 태그의 type="submit" 속성을 활용하여 동작한다.

1. <button> 태그를 활용한 버튼 생성
HTML에서 버튼을 생성할 때 가장 많이 사용하는 태그는 <button>이다.
이 태그는 텍스트, 아이콘, 이미지 등을 포함할 수 있어 유연성이 높다.

<button type="button">클릭하세요</button>
속성

type="button" → 기본 버튼 (폼 제출 기능 없음)
type="submit" → 폼 데이터를 제출
type="reset" → 입력 값을 초기화
2. <input type="submit">을 이용한 폼 제출
폼을 제출하는 가장 기본적인 방식은 <input> 태그를 활용하는 것이다.

<form action="/submit" method="post">
  <label for="username">이름:</label>
  <input type="text" id="username" name="username" required />

  <input type="submit" value="제출" />
</form>
속성

type="submit" → 폼을 제출하는 버튼
value="제출" → 버튼의 표시 텍스트 변경
활용 예시

회원가입 폼 제출: 사용자가 입력한 데이터를 서버로 전송
3. <input type="reset">을 이용한 입력 초기화
입력된 내용을 한 번에 초기화할 때 사용한다.

<form>
  <label for="email">이메일:</label>
  <input type="email" id="email" name="email" />

  <input type="reset" value="초기화" />
</form>
활용 예시

설정 변경 시 초기화 버튼 제공: 사용자가 변경한 값을 원래대로 되돌리고 싶을 때 유용.
4. <button type="submit">을 이용한 폼 제출
기본적으로 <button> 태그의 type 속성을 "submit"으로 설정하면
폼 데이터를 서버로 전송할 수 있다.

<form action="/save" method="post">
  <label for="nickname">닉네임:</label>
  <input type="text" id="nickname" name="nickname" />

  <button type="submit">저장</button>
</form>
차이점

<input type="submit"> → 단순한 제출 버튼
<button type="submit"> → 내부에 아이콘, 이미지, HTML 요소 추가 가능
5. 버튼을 활용한 JavaScript 이벤트 처리
폼을 제출하지 않고 특정 기능을 실행하고 싶다면,
JavaScript를 활용하여 버튼 클릭 이벤트를 제어할 수 있다.

<button onclick="alert('버튼이 클릭되었습니다!')">알림창 띄우기</button>
또한, 폼 제출을 JavaScript로 직접 처리할 수도 있다.

<form id="gameForm">
  <label for="score">점수 입력:</label>
  <input type="number" id="score" name="score" />

  <button type="button" onclick="submitScore()">점수 제출</button>
</form>

<script>
  function submitScore() {
    let score = document.getElementById("score").value;
    alert("제출된 점수: " + score);
  }
</script>
활용 예시

게임 내 점수 제출: 사용자가 자신의 최고 점수를 입력하고 제출 버튼을 누르면 JavaScript로 데이터를 처리.
학습자의 사고를 돕기 위한 질문
HTML에서 <button>과 <input type="submit">의 차이점은 무엇인가?

각 태그의 사용 목적과 기능 차이를 떠올려보라.
폼 데이터를 제출할 때 submit 버튼을 클릭하면 어떤 과정이 발생하는가?

폼이 서버로 데이터를 전송하는 과정을 고려해보라.
실습 문제
문제 1: 버튼을 활용한 간단한 로그인 폼 만들기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<form> 태그를 사용하여 간단한 로그인 폼을 만든다.
사용자 아이디와 비밀번호 입력 필드를 포함한다.
<input type="submit">을 사용하여 "로그인" 버튼을 추가한다.
<button> 태그를 사용하여 "회원가입" 버튼을 추가한다.
문제 2: 버튼을 사용하여 이벤트 처리하기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<button> 태그를 사용하여 "클릭하세요" 버튼을 만든다.
버튼을 클릭하면 화면에 "버튼이 클릭되었습니다!"라는 메시지가 표시되도록 설정한다.
JavaScript를 사용하여 버튼 클릭 이벤트를 처리한다.
7.4. 드롭다운 메뉴와 다중 줄 입력
HTML에서 사용자의 입력을 받기 위해 제공되는 주요 폼 요소 중 드롭다운 메뉴(select) 와 다중 줄 텍스트 입력(textarea) 은
선택 가능한 옵션 목록을 제공하거나 긴 텍스트를 입력할 수 있도록 돕는다.
이러한 요소들은 웹사이트, 게임 UI, 관리 시스템 등에서 필수적으로 사용된다.

1. <select> 태그를 활용한 드롭다운 메뉴
<select> 태그는 여러 개의 옵션 중 하나 또는 다수를 선택할 수 있도록 한다.
기본적으로 단일 선택을 지원하지만 multiple 속성을 추가하면 여러 개의 값을 선택할 수도 있다.

<label for="character">캐릭터 선택:</label>
<select id="character" name="character">
  <option value="warrior">전사</option>
  <option value="mage">마법사</option>
  <option value="archer">궁수</option>
</select>
속성

<option value="값">표시 텍스트</option> → 각 옵션을 정의
selected → 기본 선택 옵션 설정 가능
disabled → 선택 불가능한 옵션 설정
multiple → 다중 선택 가능 (Ctrl 또는 Shift 키 필요)
2. <select> 태그에서 기본 옵션 설정
기본적으로 특정 옵션이 선택되도록 설정할 수도 있다.
예를 들어, "마법사"가 기본 선택되도록 하려면 selected 속성을 사용한다.

<select name="class">
  <option value="warrior">전사</option>
  <option value="mage" selected>마법사</option>
  <option value="archer">궁수</option>
</select>
3. <select>에서 다중 선택 허용 (multiple 속성 활용)
게임에서 여러 개의 속성을 동시에 선택하도록 만들 때 유용하다.

<label for="skills">스킬 선택:</label>
<select id="skills" name="skills" multiple>
  <option value="fireball">화염구</option>
  <option value="icebolt">얼음 화살</option>
  <option value="thunder">번개</option>
</select>
위 예제에서 사용자는 Ctrl(Windows) 또는 Command(Mac) 키를 누르면서 여러 개의 옵션을 선택할 수 있다.

4. <textarea> 태그를 활용한 다중 줄 입력
사용자로부터 긴 텍스트 입력을 받을 때는 <textarea> 태그를 사용한다.
이는 게임 내 대사 입력, 버그 리포트, 설명 입력 필드 등에 활용될 수 있다.

<label for="feedback">게임 피드백:</label>
<textarea id="feedback" name="feedback" rows="4" cols="50">
여기에 내용을 입력하세요.
</textarea>
속성

rows="4" → 입력 가능한 행(row) 개수 설정
cols="50" → 가로 길이 설정
placeholder="내용 입력" → 입력 안내 텍스트 표시
maxlength="500" → 입력 가능한 최대 글자 수 제한
5. placeholder를 활용한 사용자 가이드 추가
placeholder 속성을 사용하면 사용자가 입력하기 전 안내 메시지를 표시할 수 있다.

<textarea
  name="description"
  placeholder="이곳에 캐릭터의 배경 이야기를 입력하세요."
  rows="5"
></textarea>
6. <textarea>에 JavaScript 이벤트 추가
사용자가 입력할 때 글자 수를 카운트하여 남은 글자 수를 표시할 수 있다.
이 기능은 게임 내 대사 입력, 공지사항 작성 등에 유용하게 활용될 수 있다.

<label for="message">게임 메시지 입력:</label>
<textarea
  id="message"
  name="message"
  rows="4"
  cols="50"
  oninput="countCharacters()"
></textarea>
<p id="charCount">0/200자</p>

<script>
  function countCharacters() {
    let text = document.getElementById("message").value;
    document.getElementById("charCount").innerText = text.length + "/200자";
  }
</script>
학습자의 사고를 돕기 위한 질문
<select> 태그를 사용할 때 multiple 속성을 추가하면 어떤 변화가 있는가?

단일 선택과 다중 선택의 차이를 고려해보라.
<textarea> 태그를 사용할 때 rows와 cols 속성은 어떤 역할을 하는가?

입력 창의 크기 조절 방식을 떠올려보라.
실습 문제
문제 1: 드롭다운 메뉴를 활용한 회원가입 폼 만들기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<form> 태그를 사용하여 회원가입 폼을 만든다.
<select> 태그를 사용하여 "국가 선택" 드롭다운 메뉴를 추가한다.
사용자가 선택할 수 있도록 3개 이상의 국가 옵션을 제공한다.
multiple 속성을 사용하여 여러 개의 옵션을 선택할 수 있도록 한다.
문제 2: <textarea>를 활용한 사용자 피드백 폼 만들기
아래 요구사항을 만족하는 HTML 문서를 작성하시오.

<form> 태그를 사용하여 간단한 피드백 폼을 만든다.
<textarea> 태그를 사용하여 사용자가 200자 이내의 의견을 입력할 수 있도록 설정한다.
maxlength="200" 속성을 추가하여 입력 가능한 최대 글자 수를 제한한다.
연습 문제
문제 1: HTML 문서의 기본 구조 작성하기
다음 요구사항을 만족하는 HTML 문서를 작성하시오.

<!DOCTYPE html> 선언을 포함하여 문서가 HTML5 문법을 따르도록 한다.
<html> 태그 내부에 <head>와 <body> 태그를 올바르게 포함한다.
<title> 태그를 사용하여 페이지 제목을 "HTML 연습 페이지"로 설정한다.
<body> 태그 내부에는 "이것은 HTML 기본 구조입니다."라는 문장을 표시하는 요소를 추가한다.
문제 2: <head> 태그의 구성 요소 활용하기
다음 요구사항을 만족하는 HTML 문서를 작성하시오.

<meta charset="UTF-8">을 추가하여 문서의 문자 인코딩을 UTF-8로 설정한다.
<meta> 태그를 사용하여 웹페이지의 설명(description)을 "HTML 연습 페이지입니다."로 설정한다.
<link> 태그를 사용하여 외부 CSS 파일(styles.css)을 연결한다.
<script> 태그를 사용하여 외부 JavaScript 파일(script.js)을 연결한다.
문제 3: 제목 태그 활용하기
다음 요구사항을 만족하는 HTML 문서를 작성하시오.

<h1> 태그를 사용하여 웹페이지의 대표 제목을 추가한다.
<h2> 태그를 사용하여 "소개" 섹션을 추가한다.
<h3> 태그를 사용하여 "기본 개념"이라는 소제목을 추가한다.
<h4> 태그 이하를 사용하여 추가적인 세부 정보를 설명하는 제목을 추가한다.
모든 제목 태그를 계층 구조에 맞게 배치한다.
문제 4: 단락 및 줄바꿈 태그 활용하기
다음 요구사항을 만족하는 HTML 문서를 작성하시오.

<p> 태그를 사용하여 두 개의 문단을 작성한다.
첫 번째 문단에는 "HTML은 웹 문서의 구조를 정의합니다."라는 문장을 포함한다.
두 번째 문단에는 "CSS는 웹 문서의 디자인을 적용합니다."라는 문장을 포함한다.
첫 번째 문단 안에서 <br> 태그를 사용하여 문장을 줄바꿈한다.
두 문단 사이에는 <hr> 태그를 사용하여 구분선을 추가한다.
문제 5: 강조 태그 활용하기
다음 요구사항을 만족하는 HTML 문서를 작성하시오.

<strong> 태그를 사용하여 "중요한 개념"이라는 단어를 강조한다.
<em> 태그를 사용하여 "주의해야 할 사항"이라는 문구를 기울임 처리한다.
<strong>과 <em>을 함께 사용하여 "매우 중요한 내용"이라는 문장을 강조한다.
문제 6: 하이퍼링크 생성하기
다음 요구사항을 만족하는 HTML 문서를 작성하시오.

<a> 태그를 사용하여 "네이버" (https://www.naver.com)로 이동하는 링크를 생성한다.
링크 클릭 시 새 창에서 열리도록 target="_blank" 속성을 추가한다.
현재 HTML 문서 내에서 특정 섹션(id="about")으로 이동하는 내부 링크를 추가한다.
문제 7: 이미지 삽입하기
다음 요구사항을 만족하는 HTML 문서를 작성하시오.

<img> 태그를 사용하여 images/sample.jpg 경로의 이미지를 삽입한다.
alt 속성을 설정하여 "샘플 이미지"라는 설명을 추가한다.
이미지의 너비를 500px, 높이를 350px로 설정한다.
문제 8: 리스트 작성하기
다음 요구사항을 만족하는 HTML 문서를 작성하시오.

<ul> 태그를 사용하여 "좋아하는 음식 목록"을 작성한다.
<ol> 태그를 사용하여 "아침 루틴" 목록을 작성한다.
<dl> 태그를 사용하여 "웹 개발 용어집"을 작성한다.
<dt> 태그에는 용어(예: HTML, CSS, JavaScript)를 작성한다.
<dd> 태그에는 해당 용어의 간단한 설명을 추가한다.
문제 9: 테이블 작성하기
다음 요구사항을 만족하는 HTML 문서를 작성하시오.

<table> 태그를 사용하여 학생 성적표를 만든다.
<tr> 태그를 사용하여 3명 이상의 학생 정보를 포함한다.
<th> 태그를 사용하여 "이름", "국어", "영어", "수학"의 열 제목을 작성한다.
<td> 태그를 사용하여 학생별 성적을 입력한다.
border="1" 속성을 사용하여 테두리가 보이도록 설정한다.
문제 10: 폼 요소 활용하기
다음 요구사항을 만족하는 HTML 문서를 작성하시오.

<form> 태그를 사용하여 사용자 입력 폼을 생성한다.
<input> 태그를 사용하여 다음 항목을 포함한다.
사용자 이름 입력 (텍스트 필드)
비밀번호 입력 (비밀번호 필드)
생년월일 입력 (날짜 필드)
<select> 태그를 사용하여 "국가 선택" 드롭다운 메뉴를 추가한다.
<textarea> 태그를 사용하여 200자 이내의 의견을 입력할 수 있도록 설정한다.
<button> 태그를 사용하여 "제출" 버튼을 추가한다.
답안
1. 웹의 동작 원리
1.1. HTML, CSS, JavaScript의 역할
1.1.1 질문에 대한 답안
HTML, CSS, JavaScript가 각각 담당하는 역할은 무엇인가?

HTML은 웹 페이지의 구조를 정의하는 언어로, 텍스트, 이미지, 링크 등 다양한 요소를 배치하는 역할을 한다.
CSS는 HTML 요소에 스타일을 적용하는 언어로, 색상, 글꼴, 레이아웃을 조정하여 웹사이트의 디자인을 담당한다.
JavaScript는 웹 페이지에 동적인 기능을 추가하는 언어로, 버튼 클릭 이벤트, 데이터 처리, 애니메이션 효과 등을 담당한다.
HTML 문서에서 CSS와 JavaScript를 분리하여 작성하는 것이 유지보수에 왜 유리한가?

CSS와 JavaScript를 외부 파일로 분리하면 코드의 재사용성이 높아지고 유지보수가 쉬워진다.
HTML 코드가 깔끔해지고 가독성이 향상되며, 여러 페이지에서 동일한 스타일과 스크립트를 쉽게 적용할 수 있다.
캐싱을 활용하여 페이지 로딩 속도를 개선할 수 있다.
1.2. 브라우저의 렌더링 과정
1.2.1 질문에 대한 답안
웹 브라우저가 HTML, CSS, JavaScript 파일을 처리하는 과정은 어떻게 되는가?

브라우저는 먼저 HTML 파일을 받아 DOM(Document Object Model)을 생성한다.
CSS 파일을 읽어 CSSOM(CSS Object Model)을 만든 후, DOM과 결합하여 렌더링 트리를 구성한다.
JavaScript는 실행되면서 DOM을 조작하거나 사용자 이벤트를 처리하는 역할을 한다.
마지막으로 브라우저는 렌더링 트리를 기반으로 화면에 요소들을 배치하고, 화면에 출력(rendering)한다.
브라우저에서 JavaScript 실행이 CSS 렌더링에 영향을 줄 수 있는 이유는 무엇인가?

JavaScript는 기본적으로 HTML과 CSS가 로드된 후 실행되지만, document.write()나 DOM 조작을 수행하는 경우 렌더링 과정을 차단할 수 있다.
JavaScript 파일이 <head>에 위치할 경우, 브라우저가 JavaScript 실행을 기다리는 동안 HTML과 CSS 렌더링이 지연될 수 있다.
이를 방지하기 위해 <script> 태그에 defer 또는 async 속성을 추가하여 실행 방식을 조정할 수 있다.
1.3. 클라이언트-서버 모델
1.3.1 질문에 대한 답안
클라이언트와 서버가 데이터를 주고받는 과정에서 HTTP 요청과 응답의 역할은 무엇인가?

클라이언트(웹 브라우저)는 사용자의 요청을 서버로 보내고, 서버는 요청을 처리한 후 응답을 보낸다.
요청(Request)은 보통 GET, POST, PUT, DELETE 등의 메서드를 사용하여 데이터를 요청하거나 전송한다.
응답(Response)은 HTTP 상태 코드(예: 200 OK, 404 Not Found)와 함께 클라이언트가 요청한 데이터를 반환한다.
웹에서 클라이언트가 서버로 요청을 보낼 때, GET과 POST 요청의 차이는 무엇인가?

GET 요청은 URL에 데이터를 포함하여 서버로 전달하며, 캐싱이 가능하고 주로 조회 작업에 사용된다.
POST 요청은 데이터를 HTTP 본문(body)에 포함하여 서버로 전달하며, 보안성이 높고 데이터 생성 및 변경 작업에 주로 사용된다.
2. HTML 문서 구조
2.1. HTML 문서의 기본 구조
2.1.1 질문에 대한 답안
HTML 문서에서 <head>와 <body> 태그의 역할은 각각 무엇인가?

<head> 태그는 웹 문서의 메타데이터를 포함하며, CSS, JavaScript, 폰트, SEO 관련 정보 등을 설정하는 역할을 한다.
<body> 태그는 사용자가 화면에서 볼 수 있는 콘텐츠를 포함하며, 텍스트, 이미지, 링크, 버튼 등의 요소가 위치한다.
웹 브라우저가 HTML 문서를 해석할 때 <!DOCTYPE html> 선언이 필요한 이유는 무엇인가?

<!DOCTYPE html>은 문서가 HTML5 표준을 따르고 있음을 명시하여, 브라우저가 최신 표준에 맞게 페이지를 해석하도록 돕는다.
선언하지 않으면 브라우저가 문서를 "쿼크 모드(Quirks Mode)"로 렌더링하여 예상치 못한 스타일 오류가 발생할 수 있다.
2.1.2 실습 문제에 대한 답안
문제 1: HTML 문서의 기본 구조 작성하기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>내 첫 번째 웹 페이지</title>
  </head>
  <body>
    <h1>안녕하세요!</h1>
    <p>이것은 HTML 기본 구조를 연습하는 페이지입니다.</p>
  </body>
</html>
2.2. <head> 태그의 구성 요소
2.2.1 질문에 대한 답안
HTML 문서에서 <meta> 태그는 어떤 역할을 하는가?

<meta> 태그는 문서의 인코딩, 뷰포트 설정, 검색 엔진 최적화(SEO) 정보 등을 포함하는 역할을 한다.
예를 들어 <meta charset="UTF-8">은 문서에서 UTF-8 인코딩을 사용하여 한글을 정상적으로 표시할 수 있도록 한다.
외부 CSS 파일과 JavaScript 파일을 <head>에서 로드하는 방식은 각각 어떻게 다른가?

CSS 파일은 <link rel="stylesheet" href="style.css"> 형태로 연결되며, 브라우저가 HTML을 렌더링하기 전에 스타일을 적용할 수 있다.
JavaScript 파일은 <script src="script.js"></script> 형태로 연결되며, 기본적으로 HTML과 CSS가 모두 로드된 후 실행된다.
2.2.2 실습 문제에 대한 답안
문제 1: <head> 태그 활용하기

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>HTML 문서 연습</title>
    <link rel="stylesheet" href="style.css">
    <script src="script.js"></script>
</head>
<body>
    <h1>HTML 문서 연습</h1>
    <p>이 페이지는 `<head>` 태그의 요소들을 학습하기 위한 예제입니다.</p>
</body>
</html>
2.3. <body> 태그의 역할
2.3.1 질문에 대한 답안
웹 문서에서 <body> 태그 내부에 어떤 요소들이 포함될 수 있는가?

<body> 태그 내부에는 제목(<h1>~<h6>), 문단(<p>), 이미지(<img>), 링크(<a>), 버튼(<button>), 폼(<form>) 등 다양한 요소가 포함될 수 있다.
HTML 문서에서 <body> 태그를 생략하면 어떤 문제가 발생할 수 있는가?

브라우저는 암묵적으로 <body> 태그를 생성하여 콘텐츠를 표시하지만, 예상치 못한 레이아웃 오류나 스타일 적용 문제를 유발할 수 있다.
2.3.2 실습 문제에 대한 답안
문제 1: <body> 태그 활용하기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>내 첫 번째 웹 페이지</title>
  </head>
  <body>
    <h1>내 첫 번째 웹 페이지</h1>
    <p>이 웹 페이지는 HTML 기본 구조를 연습하는 예제입니다.</p>
    <img src="sample.jpg" alt="샘플 이미지" />
    <a href="https://www.example.com">자세히 보기</a>
  </body>
</html>
3. 텍스트 관련 태그
3.1. 제목 태그 (<h1> ~ <h6>)
3.1.1 질문에 대한 답안
HTML에서 <h1>부터 <h6>까지의 태그는 각각 어떤 용도로 사용되는가?

<h1>은 문서의 가장 중요한 제목을 나타내며, <h2>~<h6>는 점점 낮은 중요도의 제목을 나타낸다.
일반적으로 <h1>은 문서의 메인 제목, <h2>는 주요 섹션 제목, <h3>~<h6>는 하위 섹션의 제목으로 사용된다.
웹 접근성을 고려할 때, 제목 태그를 적절하게 배치하는 것이 중요한 이유는 무엇인가?

시각 장애가 있는 사용자는 스크린 리더를 통해 제목을 탐색하므로, 논리적인 계층 구조를 유지하면 문서 내비게이션이 쉬워진다.
검색 엔진 최적화(SEO)에서도 제목 태그는 중요한 요소이며, <h1> 태그를 문서 내 한 번만 사용하는 것이 권장된다.
3.1.2 실습 문제에 대한 답안
문제 1: 제목 태그 사용하기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>제목 태그 연습</title>
  </head>
  <body>
    <h1>웹 개발 기초</h1>
    <h2>HTML 기본 구조</h2>
    <h3>문서의 구조</h3>
    <h4>문단과 텍스트 스타일</h4>
    <h5>리스트 태그</h5>
    <h6>참고 자료</h6>
  </body>
</html>
3.2. 단락 태그 (<p>)
3.2.1 질문에 대한 답안
HTML에서 <p> 태그가 존재하는 이유는 무엇인가?

<p> 태그는 문서를 논리적인 단락으로 구분하여 가독성을 높이는 역할을 한다.
줄바꿈 없이 텍스트를 연속적으로 표시하는 것보다 명확한 구분이 가능하여 사용자 경험을 향상시킨다.
줄바꿈 없이 텍스트를 구분할 때 <p> 태그 대신 사용할 수 있는 방법은 무엇인가?

CSS의 margin 또는 padding 속성을 활용하여 문단 간 간격을 조정할 수 있다.
<div> 태그를 사용하여 논리적인 그룹을 만들고 스타일을 적용하는 방법도 있다.
3.2.2 실습 문제에 대한 답안
문제 1: 단락 태그 활용하기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>단락 태그 연습</title>
  </head>
  <body>
    <p>안녕하세요. 저는 웹 개발을 공부하고 있습니다.</p>
    <p>제 취미는 프로그래밍과 게임 개발입니다.</p>
  </body>
</html>
3.3. 줄바꿈 및 구분선 (<br>, <hr>)
3.3.1 질문에 대한 답안
<br> 태그와 <p> 태그를 사용할 때, 각각의 차이점은 무엇인가?

<br> 태그는 줄바꿈을 적용하는 역할을 하지만, 문단을 구분하지 않는다.
<p> 태그는 문단을 논리적으로 구분하며, 자동으로 위아래 여백이 포함된다.
<hr> 태그를 문서에서 사용하면 어떤 효과가 있는가?

<hr> 태그는 문서 내 섹션을 구분하는 가로선을 삽입하여 시각적으로 구분할 수 있도록 한다.
주제 변경, 문서의 구획을 강조할 때 유용하다.
3.3.2 실습 문제에 대한 답안
문제 1: 줄바꿈과 구분선 적용하기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>줄바꿈 및 구분선 연습</title>
  </head>
  <body>
    <p>안녕하세요.<br />저는 웹 개발을 공부하고 있습니다.</p>
    <hr />
    <p>아래는 HTML의 기본적인 요소들입니다.</p>
  </body>
</html>
3.4. 강조 태그 (<strong>, <em>)
3.4.1 질문에 대한 답안
<strong> 태그와 <em> 태그의 차이점은 무엇인가?

<strong> 태그는 중요한 텍스트를 강조하며, 기본적으로 굵게 표시된다.
<em> 태그는 강조의 의미를 포함하며, 기본적으로 기울여진 텍스트로 표시된다.
텍스트를 강조하는 방법으로 CSS 스타일링 대신 HTML 태그를 사용하는 이유는 무엇인가?

의미론적 마크업을 통해 검색 엔진과 스크린 리더가 내용을 올바르게 이해할 수 있도록 돕는다.
CSS 스타일은 단순한 시각적 효과만 제공하지만, <strong>과 <em> 태그는 의미를 강조하는 역할도 수행한다.
3.4.2 실습 문제에 대한 답안
문제 1: 강조 태그 적용하기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>강조 태그 연습</title>
  </head>
  <body>
    <p>
      <strong>중요한 정보:</strong> 웹 개발을 공부하는 것은 매우 중요합니다.
    </p>
    <p><em>강조된 문장:</em> HTML과 CSS를 배워야 합니다.</p>
  </body>
</html>
4. 하이퍼링크 및 이미지 삽입
4.1. 하이퍼링크 생성 (<a>)
4.1.1 질문에 대한 답안
<a> 태그를 사용할 때 href 속성이 하는 역할은 무엇인가?

href 속성은 하이퍼링크가 이동할 목적지를 지정하는 역할을 한다.
내부 페이지 이동, 외부 웹사이트 이동, 이메일 전송, 파일 다운로드 등의 기능을 수행할 수 있다.
target="_blank" 속성을 사용하면 어떤 효과가 발생하는가?

target="_blank" 속성을 추가하면 링크를 새 창이나 새 탭에서 열 수 있다.
사용자 경험을 개선할 수 있지만, 보안적인 이유로 rel="noopener noreferrer"를 함께 사용하는 것이 권장된다.
4.1.2 실습 문제에 대한 답안
문제 1: 하이퍼링크 생성하기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>하이퍼링크 연습</title>
  </head>
  <body>
    <p>
      <a href="https://www.naver.com" target="_blank" rel="noopener noreferrer"
        >네이버로 이동</a
      >
    </p>
    <p><a href="#section1">본문의 특정 섹션으로 이동</a></p>

    <h2 id="section1">여기는 본문 섹션입니다.</h2>
  </body>
</html>
4.2. 이미지 삽입 (<img>)
4.2.1 질문에 대한 답안
웹 페이지에서 <img> 태그의 alt 속성이 중요한 이유는 무엇인가?

alt 속성은 이미지가 로드되지 않을 경우 대체 텍스트를 제공한다.
웹 접근성을 향상시키며, 시각 장애가 있는 사용자가 화면 리더를 통해 이미지를 이해할 수 있도록 돕는다.
검색 엔진 최적화(SEO)에도 긍정적인 영향을 준다.
이미지 파일을 로드할 때 경로 설정이 잘못되면 어떻게 되는가?

이미지가 표시되지 않으며, 브라우저에서는 대체 텍스트(alt 속성의 값)가 출력된다.
절대 경로와 상대 경로를 올바르게 설정해야 하며, 외부 이미지 URL을 사용할 경우 인터넷 연결 상태를 고려해야 한다.
4.2.2 실습 문제에 대한 답안
문제 1: 이미지 삽입하기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>이미지 삽입 연습</title>
  </head>
  <body>
    <h1>웹 개발 학습</h1>
    <img src="images/sample.jpg" alt="샘플 이미지" width="300" />
  </body>
</html>
5. 목록 태그 (리스트 요소)
5.1. 순서 없는 목록 (<ul>, <li>)
5.1.1 질문에 대한 답안
순서 없는 목록(<ul>)과 순서 있는 목록(<ol>)의 차이는 무엇인가?

<ul> 태그는 항목 앞에 기호(●, ○, ■ 등)를 사용하여 목록을 나타낸다.
<ol> 태그는 항목 앞에 숫자(1, 2, 3...) 또는 알파벳(A, B, C...)을 사용하여 목록을 나타낸다.
HTML 문서에서 <ul> 태그를 사용하면 어떤 시각적 효과가 나타나는가?

브라우저에서 기본적으로 점 모양의 불릿 포인트가 나타난다.
CSS를 활용하여 불릿 스타일을 변경하거나 없앨 수도 있다.
5.1.2 실습 문제에 대한 답안
문제 1: 순서 없는 목록 만들기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>순서 없는 목록 연습</title>
  </head>
  <body>
    <h2>내가 좋아하는 음식</h2>
    <ul>
      <li>피자</li>
      <li>초밥</li>
      <li>파스타</li>
    </ul>
  </body>
</html>
5.2. 순서 있는 목록 (<ol>, <li>)
5.2.1 질문에 대한 답안
순서 있는 목록(<ol>)을 사용하면 어떤 장점이 있는가?

항목 간의 순서를 강조해야 할 때 유용하다.
예를 들어, 조리법, 절차 설명, 단계별 가이드를 작성할 때 적절하다.
HTML 문서에서 <ol> 태그의 기본 번호 매김 방식을 변경하는 방법은 무엇인가?

type 속성을 사용하여 숫자(1, 2, 3), 알파벳(A, B, C), 로마 숫자(I, II, III) 등으로 변경할 수 있다.
start 속성을 사용하여 시작 번호를 조정할 수도 있다.
5.2.2 실습 문제에 대한 답안
문제 1: 순서 있는 목록 만들기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>순서 있는 목록 연습</title>
  </head>
  <body>
    <h2>아침 루틴</h2>
    <ol>
      <li>기상 후 스트레칭</li>
      <li>샤워하기</li>
      <li>아침 식사</li>
      <li>출근 준비</li>
      <li>집에서 나가기</li>
    </ol>
  </body>
</html>
5.3. 정의 목록 (<dl>, <dt>, <dd>)
5.3.1 질문에 대한 답안
정의 목록(<dl>)을 사용할 때 적절한 예시는 무엇인가?

용어와 그에 대한 설명을 제공하는 경우 사용된다.
예를 들어, 웹 개발 용어집, FAQ(자주 묻는 질문과 답변), 사전 항목 등이 있다.
정의 목록(<dl>, <dt>, <dd>)이 <ul> 또는 <ol>과 다른 점은 무엇인가?

<ul>과 <ol>은 단순한 목록을 나타내는 반면, <dl>은 용어와 설명을 연결하는 역할을 한다.
5.3.2 실습 문제에 대한 답안
문제 1: 정의 목록 만들기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>정의 목록 연습</title>
  </head>
  <body>
    <h2>웹 개발 용어집</h2>
    <dl>
      <dt>HTML</dt>
      <dd>웹 페이지의 구조를 정의하는 마크업 언어</dd>
      <dt>CSS</dt>
      <dd>웹 페이지의 스타일을 지정하는 스타일시트 언어</dd>
      <dt>JavaScript</dt>
      <dd>웹 페이지에 동적인 기능을 추가하는 프로그래밍 언어</dd>
    </dl>
  </body>
</html>
6. 테이블 구성
6.1. 테이블 태그의 기본 구조
6.1.1 질문에 대한 답안
HTML 테이블을 사용할 때 <tr>, <th>, <td> 태그의 역할은 무엇인가?

<tr> 태그는 테이블의 행(row)을 생성한다.
<th> 태그는 테이블의 헤더 셀을 정의하며 기본적으로 글씨가 굵고 가운데 정렬된다.
<td> 태그는 일반 데이터 셀을 정의하며 기본적으로 왼쪽 정렬된다.
테이블을 활용할 때 CSS로 스타일을 조정할 수 있는 요소에는 어떤 것들이 있는가?

border: 테두리 스타일을 지정한다.
cellpadding: 셀 내부 여백을 지정한다.
cellspacing: 셀 간격을 지정한다.
text-align: 텍스트 정렬을 설정한다.
background-color: 배경색을 지정한다.
6.1.2 실습 문제에 대한 답안
문제 1: 기본 테이블 만들기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>기본 테이블 연습</title>
  </head>
  <body>
    <h2>학생 성적표</h2>
    <table border="1">
      <tr>
        <th>이름</th>
        <th>수학</th>
        <th>영어</th>
        <th>과학</th>
      </tr>
      <tr>
        <td>김철수</td>
        <td>85</td>
        <td>90</td>
        <td>80</td>
      </tr>
      <tr>
        <td>이영희</td>
        <td>95</td>
        <td>88</td>
        <td>92</td>
      </tr>
    </table>
  </body>
</html>
6.2. 테이블 속성 활용
6.2.1 질문에 대한 답안
테이블에서 colspan과 rowspan 속성은 각각 어떤 역할을 하는가?

colspan 속성은 여러 열(column)을 하나의 셀로 병합할 때 사용한다.
rowspan 속성은 여러 행(row)을 하나의 셀로 병합할 때 사용한다.
border, cellpadding, cellspacing 속성을 사용할 때 시각적으로 어떤 효과가 나타나는가?

border: 테이블의 테두리를 표시하거나 감춘다.
cellpadding: 셀 내부의 여백을 추가하여 가독성을 높인다.
cellspacing: 셀 사이의 간격을 조절하여 테이블의 디자인을 개선한다.
6.2.2 실습 문제에 대한 답안
문제 1: 셀 병합이 포함된 테이블 만들기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>셀 병합 테이블</title>
  </head>
  <body>
    <h2>시간표</h2>
    <table border="1">
      <tr>
        <th>시간</th>
        <th>월요일</th>
        <th>화요일</th>
        <th>수요일</th>
      </tr>
      <tr>
        <td>9:00 - 10:00</td>
        <td rowspan="2">수학</td>
        <td>영어</td>
        <td>국어</td>
      </tr>
      <tr>
        <td>10:00 - 11:00</td>
        <td colspan="2">과학</td>
      </tr>
    </table>
  </body>
</html>
7. 폼 요소와 사용자 입력 태그
7.1. <form> 태그의 역할
7.1.1 질문에 대한 답안
HTML에서 <form> 태그의 기본 역할은 무엇인가?

사용자 입력을 받아 서버로 전송하는 역할을 한다.
다양한 입력 필드를 포함할 수 있으며, action 속성을 통해 데이터 전송 대상 URL을 지정할 수 있다.
폼 데이터를 전송할 때 GET과 POST 방식의 차이점은 무엇인가?

GET 방식은 URL에 데이터를 포함하여 전송하며, 보안성이 낮지만 빠른 요청이 가능하다.
POST 방식은 본문(body)에 데이터를 포함하여 전송하며, 보안성이 높고 대용량 데이터를 전송할 수 있다.
7.2. 다양한 <input> 타입
7.2.1 질문에 대한 답안
HTML <input> 태그의 다양한 타입에는 어떤 것들이 있는가?

type="text": 일반 텍스트 입력
type="password": 비밀번호 입력
type="radio": 라디오 버튼
type="checkbox": 체크박스
type="number": 숫자 입력
type="date": 날짜 선택
사용자가 올바른 데이터를 입력하도록 도와주는 HTML 속성은 무엇인가?

placeholder: 입력 필드에 안내 문구를 표시한다.
required: 필수 입력 필드로 설정한다.
maxlength: 입력 가능한 최대 글자 수를 제한한다.
7.2.2 실습 문제에 대한 답안
문제 1: 다양한 입력 필드 포함한 폼 만들기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>입력 필드 연습</title>
  </head>
  <body>
    <h2>회원가입 폼</h2>
    <form>
      <label>이름: <input type="text" name="name" required /></label><br />
      <label>비밀번호: <input type="password" name="password" required /></label
      ><br />
      <label>생년월일: <input type="date" name="birthdate" /></label><br />
      <label
        >성별: <input type="radio" name="gender" value="male" /> 남성
        <input type="radio" name="gender" value="female" /> 여성 </label
      ><br />
      <label
        >관심 분야:
        <input type="checkbox" name="interest" value="coding" /> 코딩
        <input type="checkbox" name="interest" value="music" /> 음악 </label
      ><br />
      <input type="submit" value="가입하기" />
    </form>
  </body>
</html>
7.3. 버튼과 폼 제출 (<button>, <input type="submit">)
7.3.1 질문에 대한 답안
HTML에서 <button>과 <input type="submit">의 차이점은 무엇인가?

<button> 태그는 내부에 HTML 요소를 포함할 수 있으며, 자바스크립트와 연동하여 다양한 기능을 추가할 수 있다.
<input type="submit"> 태그는 폼 데이터를 서버로 전송하는 기본 기능을 수행하며, 추가적인 HTML 요소를 포함할 수 없다.
폼 데이터를 제출할 때 submit 버튼을 클릭하면 어떤 과정이 발생하는가?

사용자가 버튼을 클릭하면 폼의 action 속성에 지정된 URL로 입력 데이터가 전송된다.
전송 방식(GET 또는 POST)에 따라 URL에 데이터가 추가되거나 요청 본문에 포함된다.
서버가 요청을 처리한 후, 응답 데이터를 클라이언트에 반환한다.
7.3.2 실습 문제에 대한 답안
문제 1: 버튼을 활용한 간단한 로그인 폼 만들기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>로그인 폼</title>
  </head>
  <body>
    <h2>로그인</h2>
    <form action="login.php" method="post">
      <label>아이디: <input type="text" name="username" required /></label
      ><br />
      <label>비밀번호: <input type="password" name="password" required /></label
      ><br />
      <input type="submit" value="로그인" />
      <button type="button" onclick="alert('회원가입 페이지로 이동합니다.')">
        회원가입
      </button>
    </form>
  </body>
</html>
문제 2: 버튼을 사용하여 이벤트 처리하기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>버튼 이벤트</title>
    <script>
      function showMessage() {
        alert("버튼이 클릭되었습니다!");
      }
    </script>
  </head>
  <body>
    <h2>버튼 클릭 이벤트</h2>
    <button onclick="showMessage()">클릭하세요</button>
  </body>
</html>
7.4. 드롭다운 메뉴와 다중 줄 입력 (<select>, <textarea>)
7.4.1 질문에 대한 답안
<select> 태그를 사용할 때 multiple 속성을 추가하면 어떤 변화가 있는가?

기본적으로 드롭다운에서 단일 선택만 가능하지만, multiple 속성을 추가하면 여러 개의 항목을 동시에 선택할 수 있다.
<textarea> 태그를 사용할 때 rows와 cols 속성은 어떤 역할을 하는가?

rows 속성은 입력 필드의 세로(행) 크기를 조정하고, cols 속성은 가로(열) 크기를 조정한다.
7.4.2 실습 문제에 대한 답안
문제 1: 드롭다운 메뉴를 활용한 회원가입 폼 만들기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>회원가입 폼</title>
  </head>
  <body>
    <h2>회원가입</h2>
    <form>
      <label>이름: <input type="text" name="name" required /></label><br />
      <label
        >국가 선택:
        <select name="country">
          <option value="kr">대한민국</option>
          <option value="us">미국</option>
          <option value="jp">일본</option>
        </select> </label
      ><br />
      <label
        >취미 선택 (다중 선택 가능):
        <select name="hobby" multiple>
          <option value="reading">독서</option>
          <option value="sports">운동</option>
          <option value="music">음악</option>
        </select> </label
      ><br />
      <input type="submit" value="가입하기" />
    </form>
  </body>
</html>
문제 2: <textarea>를 활용한 사용자 피드백 폼 만들기

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>피드백 폼</title>
  </head>
  <body>
    <h2>사용자 피드백</h2>
    <form>
      <label>의견을 작성해주세요:</label><br />
      <textarea
        name="feedback"
        rows="5"
        cols="40"
        maxlength="200"
        placeholder="최대 200자까지 입력 가능합니다."
      ></textarea
      ><br />
      <input type="submit" value="제출" />
    </form>
  </body>
</html>
8. 연습 문제에 대한 답안
8.1 HTML 문서의 기본 구조 작성하기

정답:
HTML 문서의 기본 구조를 올바르게 작성한다.

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>HTML 연습 페이지</title>
</head>
<body>
    <p>이것은 HTML 기본 구조입니다.</p>
</body>
</html>
8.2 <head> 태그의 구성 요소 활용하기

정답:
메타데이터, 외부 스타일시트 및 스크립트를 포함한 <head> 태그를 작성한다.

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="description" content="HTML 연습 페이지입니다.">
    <title>HTML 연습 페이지</title>
    <link rel="stylesheet" href="styles.css">
    <script src="script.js"></script>
</head>
<body>
</body>
</html>
8.3 제목 태그 활용하기

정답:
제목 태그를 계층적으로 올바르게 배치한다.

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>제목 태그 연습</title>
</head>
<body>
    <h1>웹 개발 학습</h1>
    <h2>소개</h2>
    <h3>기본 개념</h3>
    <h4>세부 정보</h4>
    <h5>추가 설명</h5>
    <h6>마무리</h6>
</body>
</html>
8.4 단락 및 줄바꿈 태그 활용하기

정답:
<p>, <br>, <hr> 태그를 활용하여 문장을 구성한다.

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>단락 태그 연습</title>
</head>
<body>
    <p>HTML은 웹 문서의 구조를 정의합니다.<br>
       HTML을 사용하면 문서의 제목, 단락 등을 표현할 수 있습니다.</p>

    <hr>

    <p>CSS는 웹 문서의 디자인을 적용합니다.</p>
</body>
</html>
8.5 강조 태그 활용하기

정답:
<strong>, <em> 태그를 사용하여 강조 효과를 적용한다.

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>강조 태그 연습</title>
</head>
<body>
    <p><strong>중요한 개념</strong>을 반드시 이해해야 합니다.</p>
    <p><em>주의해야 할 사항</em>을 놓치지 않도록 하세요.</p>
    <p><strong><em>매우 중요한 내용</em></strong>을 반드시 숙지하세요.</p>
</body>
</html>
8.6 하이퍼링크 생성하기

정답:
내부 및 외부 하이퍼링크를 생성한다.

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>하이퍼링크 연습</title>
</head>
<body>
    <p><a href="https://www.naver.com" target="_blank">네이버</a>로 이동</p>
    <p><a href="#about">소개 섹션으로 이동</a></p>

    <h2 id="about">소개 섹션</h2>
    <p>이 섹션은 소개 내용입니다.</p>
</body>
</html>
8.7 이미지 삽입하기

정답:
이미지를 올바르게 삽입하고 크기를 조정한다.

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>이미지 삽입 연습</title>
</head>
<body>
    <img src="images/sample.jpg" alt="샘플 이미지" width="500" height="350">
</body>
</html>
8.8 리스트 작성하기

정답:
순서 없는 목록, 순서 있는 목록, 정의 목록을 작성한다.

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>리스트 연습</title>
</head>
<body>
    <h2>좋아하는 음식 목록</h2>
    <ul>
        <li>피자</li>
        <li>초밥</li>
        <li>라면</li>
    </ul>

    <h2>아침 루틴</h2>
    <ol>
        <li>기상</li>
        <li>세수</li>
        <li>아침 식사</li>
        <li>운동</li>
        <li>출근 준비</li>
    </ol>

    <h2>웹 개발 용어집</h2>
    <dl>
        <dt>HTML</dt>
        <dd>웹 페이지의 구조를 정의하는 언어</dd>
        <dt>CSS</dt>
        <dd>웹 페이지의 스타일을 적용하는 언어</dd>
        <dt>JavaScript</dt>
        <dd>웹 페이지의 동적인 기능을 구현하는 언어</dd>
    </dl>
</body>
</html>
8.9 테이블 작성하기

정답:
학생 성적표 테이블을 작성한다.

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>테이블 연습</title>
</head>
<body>
    <h2>학생 성적표</h2>
    <table border="1">
        <tr>
            <th>이름</th>
            <th>국어</th>
            <th>영어</th>
            <th>수학</th>
        </tr>
        <tr>
            <td>홍길동</td>
            <td>90</td>
            <td>85</td>
            <td>95</td>
        </tr>
        <tr>
            <td>김영희</td>
            <td>80</td>
            <td>90</td>
            <td>88</td>
        </tr>
        <tr>
            <td>이철수</td>
            <td>85</td>
            <td>92</td>
            <td>87</td>
        </tr>
    </table>
</body>
</html>
8.10 폼 요소 활용하기

정답:
사용자 입력 폼을 작성하고 필드를 구성한다.

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>폼 요소 연습</title>
</head>
<body>
    <h2>회원가입</h2>
    <form>
        <label for="username">사용자 이름:</label>
        <input type="text" id="username" name="username"><br><br>

        <label for="password">비밀번호:</label>
        <input type="password" id="password" name="password"><br><br>

        <label for="birthdate">생년월일:</label>
        <input type="date" id="birthdate" name="birthdate"><br><br>

        <label for="country">국가 선택:</label>
        <select id="country" name="country">
            <option value="kr">대한민국</option>
            <option value="us">미국</option>
            <option value="jp">일본</option>
        </select><br><br>

        <label for="feedback">의견을 남겨주세요:</label><br>
        <textarea id="feedback" name="feedback" rows="4" cols="50" maxlength="200"></textarea><br><br>

        <button type="submit">제출</button>
    </form>
</body>
</html>
닫기
