<img width="132" height="184" alt="image" src="https://github.com/user-attachments/assets/31356185-7a88-4917-9d79-4b65c3d4d8ee" /># 웹 문서에 디자인 입히기

### 스타일과 스타일 시트

기본형은 ```선택자 { 속성1: 속성값1; 속성2: 속성값2; }```
```css 
p {
  text-align: center;
  color: blue;
}
```
--------------------
### 스타일 규칙
1. 세미콜론(;)으로 구분하여 중괄호({})안에 나열한다.
2. 스타일 속성이 여러개일 경우 한줄에 속성을 하나만 적는 것이 좋다.
3. 오른쪽에 주석(/* ~ */)을 붙여 소스 관리하는 것이 좋다.(최소한으로 하는게 파일 크기에 좋음)

-------------------------
### 인라인 스타일 시트
간단한 스타일 정보라면 스타일 시트를 사용하지 않고 적용할 대상에 직접 표시한다.<br>
```style="속성: 속성값;"```
```html
<h1>레드향</h1>
<p style="color:blue;">껍질에 붉은 빛이 돌아 레드향이라 불린다.</p>
```

------------------------
### 내부 스타일 시트
웹 문서 안에 사용할 스타일을 같은 문서 안에 정리한 것을 **내부 스타일 시트**라고한다.<br>
웹 스타일 정보는 브라우저 화면에 표시하기 전에 결정해야 하므로<br>
모든 스타일 정보는 ```<head>```태그 안에서 정의하며 ```<style>```을 사용한다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>상품 소개 페이지</title>
  <style>
    h1 {      
      padding:10px;
      background-color:#222;
      color:#fff;
    }
  </style>
</head>
<body>
  <h1>레드향</h1>
  <p>껍질에 붉은 빛이 돌아 레드향이라 불린다.
</body>
</html>
```
---------------------
### 외부 스타일 시트
사이트를 제작할 때 여러 웹 문서에서 사용할 스타일을 별도 파일로 저장해놓고 필요할 때 가져와서 사용하는 것이 일반적이다.<br>
이렇게 따로 저장해 놓은 스타일 정보를 **외부 스타일 시트**라고한다.<br>
이렇게 만든 웹 문서에 연결해야 스타일이 문서에 적용되며, ```<link>```태그를 사용한다.<br>
```<link rel="stylesheet" href="외부 스타일 시트 파일 경로">```

-----------------
### 선택자
선택자에는 여러 스타일이 있으며, 선택자에 따라 스타일의 범위가 달라진다.

#### 전체 선택자
스타일을 문서의 모든 요소에 적용할 때 사용한다. 주로 기본 스타일을 초기화할때 사용하면 좋다.
```css
* { 속성: 값;}
```

#### 클래스 선택자
클래스 선택자는 클래스 이름을 사용해서 다른 선택자와 구별하는데, 이때 클래스 이름 앞에 마침표(.)을 반드시 붙여야 한다.<br>
```.클래스명``` { 스타일 규칙 }

#### id 선택자
id선택자도 클래스 선택자와 마찬가지로 특정 부분을 선택해서 스타일을 지정할때 사용한다.<br>
마침표(.)대신 #기호를 사용한다.
```#아이디명 { 스타일 규칙 }```

클래스 선택자와 id선택자의 가장 큰 차이는<br>
**클래스 선택자가 문서에서 여러번 적용할 수 있는 반면, id선택자는 문서에서 한 번만 적용할 수 있다는 것이다.**
```html
<style>
    #container {
      width:500px;  /* 너비 */
      margin:10px auto;  /* 바깥 여백 */
      padding:10px;  /* 테두리와 내용 사이 여백 */ 
      border:1px solid #000;  /* 테두리 */
    }    
  </style>
</head>
<body>
  <div id="container">
    <h1>레드향</h1>
```

#### 그룹 선택자
같은 스타일 규칙을 사용하는 경우에는, 쉼표(,)로 구분해 여러 선택자를 나열한 후 정의한다.<br>
```선택자1, 선택자2 { 스타일 규칙 }```
```css
h1, p {
  text-align: center;
}
```

-----------
### 스타일 우선 순위
**!important -> 인라인 스타일 -> id 스타일 -> 클래스 스타일 -> 타입 스타일**

-------------------
# 글꼴 관련 스타일
### 글꼴 지정하는 font-famaily 속성
웹 문서에 지정한 글꼴이 없을 경우를 대비해서 두번째, 세번째 글꼴까지 생각해야 한다.

```font-famaily:<글꼴 이름>, <글꼴 이름>, <글꼴 이름>```
```css
body { font-family: "맑은 고딕", 돋움, 굴림 }
```

---------------------
### 글자 크기를 지정하는 font-size
```font-size: <절대 크기> | <상대 크기> | <크기> | <백분율>```

------------------
### 글자 굵기를 지정하는 font-weight
```font-weight: normal | bold | bolder | lighter | 100 | 200 |```

------------------
### 웹 폰트 사용하기
웹 폰트를 사용하려면 웹 문서를 작성할 때 글꼴 정보를 함께 저장해야 한다.<br>
웹 폰트를 사용한 사이트에 사용자가 접속하면 웹 문서를 내려받으면서 웹 폰트도 사용자 시스템으로 다운로드 된다.<br>
```css
@font-face {
  font-family: <글꼴 이름>;
  src: <글꼴 파일>;
}
```
**예시**
```html
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>웹 폰트 사용하기</title>
    <style>
      @font-face {
        font-family: 'Ostrich';  /* 폰트 이름 */
        src: local('Ostrich Sans'), 
              url('fonts/ostrich-sans-bold.woff') format('woff'), 
              url('fonts/ostrich-sans-bold.ttf') format('truetype'), 
              url('fonts/ostrich-sans-bold.svg') format('svg');
      }
      .wfont {
        font-family:'Ostrich', sans-serif; /* 웹 폰트 지정 */
      }
      p {
        font-size:30px; /* 글자 크기 */
      }
    </style>
</head>
<body>
  <p>Using Default Fonts</p>
  <p class="wfont">Using Web Fonts</p>
</body>
</html>
```
----------------
### 구글 폰트 사용하기
```html
<head>
  <meta charset="UTF-8">
  <title>구글 폰트 사용하기</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Nanum+Pen+Script&display=swap');

    h1 {
      font-size: 60px;
      font-weight: bold;
      font-family: "Nanum Pen Script", cursive;
    }
  </style>
</head>

<body>
  <h1>HTML+CSS+JavaScript</h1>
</body>
```

--------------------
# 텍스트 관련 스타일
웹 문서에서 문단이나 제목 등의 텍스트에서 글자색을 바꿀 때는 color 속성을 사용한다.
```css
color: <색상>
```

### 16진수로 표현하는 법
6자리의 16진수는 앞에서부터 두자리씩 묶어 **#RRGGBB**로 표시된다.
```css
p {
  color: #034f1f;
}
```

### hsl과 hsla로 표현하는 법
hue(색상), saturation(채도), lightness(명도)의 줄임말이다.
```css
p {
  color: hsl(0, 100%, 50%);
}
```

### 색상을 영문명으로 표현하는 방법
```css
p {
color: green;
}
```

### rgb, rgba 표기법
```css
h1 {
  color: rgb(0, 0, 255);
}

h2 {
  color: rgba(0, 0, 255, 0.5) # a는 alpha 불투명도의 값이다.
}
```
------------------------
### 텍스트 정렬
```css
text-align: start
```
**속성값**
|종류|설명|
|:---|:---|
|start|현재 텍스트 줄의 시작 위치에 맞추어 문단을 정렬한다.|
|end|현재 텍스트 줄의 끝 위치에 맞추어 문단을 정렬한다.|
|left|왼쪽에 맞추어 문단을 정렬한다.|
|right|오른쪽에 맞추어 문단을 정렬한다.|
|center|가운데에 맞추어 문단을 정렬한다.|
|justify| 양쪽에 맞추어 문단을 정렬한다.|
|match-parent|부모 요소를 따라 문단을 정렬한다.

--------------
### 줄 간격 조절
한 문단이 두 줄을 넘기면 줄 간격이 생긴다. 그 사이를 조절할 수 있다.
```css
p {
  font-size: 12px;
  line-height: 24px;
}
```
----------------
### 텍스트 줄 표시
```css
<p style="text-decoration:none">none</p>
<p style="text-decoration:underline">underline</p>
<p style="text-decoration:overline">overline</p>
<p style="text-decoration:line-through">line through</p>
```
<img width="132" height="184" alt="image" src="https://github.com/user-attachments/assets/738974ee-9039-4e04-9a04-e73a000a981d" />

------------------
### 텍스트 그림자 효과
```css
text-shadow: none : <가로 거리> <세로 거리> <번짐 정도> <색상>
```

**예시**
```css
<style>    
    h1 { 
      font-size:60px;
    } 
    .shadow1 {
      color:red;
      text-shadow:1px 1px black;
    }
    .shadow2 {
      text-shadow:5px 5px 3px #ffa500;
    }
    .shadow3 {
      color:#fff;
      text-shadow:7px -7px 20px #000;
    }
  </style>
```
----------------
### 텍스트 대소 문자 변환
|종류|설명|
|:---|:---|
|capitalize|첫 번째 글자를 대문자로 변환한다.|
|uppercase|모든 글자를 대문자로 변환한다.|
|lowercase|모든 글자를 소문자로 변환한다.|
|full-width|가능한 한 모든 문자를 전각 문자로 변환한다.|

```css
<style>    
    .trans1 {
      text-transform: capitalize;
    }
    .trans2 {
      text-transform: uppercase;
    }
    .trans3 {
      text-transform: lowercase;
    }
  </style>
```
-------------------
### 글자 간격 조절
letter-spacing 속성은 글자와 글자 사이의 간격을 조절<br>
word-spacting 속성은 단어와 단어 사이의 간격을 조절
```css
<style> 
  .spacing1 {
    letter-spacing:0.2em;  /* 글자 간격 0.2em */
  }
  .spacing2 {
    letter-spacing:0.5em;  /* 글자 간격 0.5em */
  }      
</style>
```
-----------------
# 목록 스타일
