# 1. OAuth2 개요
## 1-1. OAuth2의 개념
### OAuth2란 무엇인가?
OAuth2는 인터넷 서비스 간에 안전하게 권한을 위임할 수 있도록 설계된 인증 및 인가 프로토콜이다.<br>
OAuth2의 핵심 개념은 사용자(User)가 직접 로그인 정보를 공유하지 않고도, 타사 애플리케이션(클라이언트)이 특정 리소스에 대한 액세스를 요청할 수 있도록 한다는 것이다.<br>
이를 위해 OAuth2는 토큰 기반의 접근 제어 방식을 사용하며, 사용자의 민감한 정보를 보호하는 데 초점을 맞춘다.

-------------
### OAuth2의 필요성
기존의 인증 방식에서는 서비스마다 사용자 정보를 개별적으로 저장하고 관리해야 했다.<br>
예를 들어, 사용자가 여러 개의 웹사이트에서 동일한 이메일 주소와 비밀번호를 사용해야 한다면, 보안적으로 큰 취약점이 발생할 수 있다. 하나의 웹사이트에서 비밀번호가 유출되면, 같은 비밀번호를 사용하는 모든 서비스가 위험해질 가능성이 있다. <br>
이를 해결하기 위해 OAuth2는 사용자 정보를 직접 제공하는 대신, 인증된 액세스 토큰을 통해 권한을 위임하는 방식을 채택했다.

이 방식은 특히 다음과 같은 이유로 중요하다:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**보안 강화**: 서비스 간의 직접적인 사용자 정보 공유 없이 안전한 접근 권한을 제공한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**편의성 증가**: 사용자들은 여러 개의 서비스에서 하나의 로그인 계정을 사용할 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**범용성 확보**: 웹, 모바일, 데스크톱 애플리케이션에서 공통적으로 사용될 수 있는 인증 방식이다.

-----------
### OAuth2의 주요 개념
OAuth2는 **권한 부여(Authorization)와 인증(Authentication)을 구분**하는 것이 특징이다. 많은 사람들이 OAuth2를 인증 프로토콜로 오해하지만, 실제로는 권한 부여를 위한 프로토콜이다.

OAuth2의 기본 개념을 이해하기 위해 다음과 같은 주요 용어를 살펴볼 필요가 있다.

**Resource Owner (리소스 소유자)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;보호된 리소스(예: 사용자의 개인 정보, 이메일, 사진 등)를 소유한 주체이다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;일반적으로 사용자를 의미하지만, 서비스 자체가 리소스 소유자가 될 수도 있다.

**Client (클라이언트)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;리소스 소유자의 동의하에 특정 리소스에 접근하고자 하는 애플리케이션이다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트는 직접 사용자 정보를 요구하지 않고, 인증 서버를 통해 접근 권한을 위임받는다.

**Authorization Server (인증 서버)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트의 액세스 요청을 처리하고, 적절한 인증 및 권한 부여를 수행하는 서버이다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;인증 서버는 사용자의 로그인 정보를 확인한 후, 해당 클라이언트에게 액세스 토큰을 발급한다.

**Resource Server (리소스 서버)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;리소스를 저장하고 있는 서버로, 클라이언트의 요청을 처리할 때 액세스 토큰을 확인하여 권한을 검증한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;예를 들어, Google Drive API는 리소스 서버 역할을 수행하며, 액세스 토큰이 유효한 경우에만 파일 데이터를 제공한다.

------------------
### OAuth2의 주요 특징
OAuth2는 기존의 인증 방식보다 다음과 같은 점에서 차별점을 가진다.

**토큰 기반 인증(Token-based Authentication)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;OAuth2는 사용자 인증 정보를 직접 노출하지 않고, 액세스 토큰을 통해 권한을 위임하는 방식을 사용한다. 이를 통해 사용자 비밀번호가 외부에 노출되는 위험을 최소화할 수 있다.

**다양한 인증 흐름(Grant Type) 제공**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;OAuth2는 다양한 환경에서 사용할 수 있도록 여러 가지 인증 방식을 제공한다. 예를 들어, 웹 애플리케이션에서는 Authorization Code Grant 방식을 주로 사용하고, 서버 간 인증을 위해 Client Credentials Grant 방식이 활용될 수 있다.

**세션 상태를 저장하지 않는 구조(Stateless Authentication)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;OAuth2를 활용하면 클라이언트와 서버 간의 세션을 유지할 필요가 없다. 대신 클라이언트는 매 요청마다 액세스 토큰을 포함하여 요청을 보내며, 서버는 토큰을 검증하여 접근을 허용할지 결정한다. 이를 통해 서버의 부하를 줄이고 확장성을 높일 수 있다.

**제3자 애플리케이션 접근 가능(Third-party Authorization)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;OAuth2를 사용하면 사용자는 자신의 계정 정보를 직접 입력하지 않고도, 타사 애플리케이션에 접근 권한을 부여할 수 있다. 예를 들어, 사용자가 Google 계정을 이용해 타사 서비스에 로그인할 수 있는 것은 OAuth2 덕분이다.

---------------
### OAuth2의 일반적인 흐름
OAuth2를 통해 클라이언트가 사용자의 리소스에 접근하는 일반적인 흐름을 간단히 정리하면 다음과 같다.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;사용자가 클라이언트 애플리케이션에서 특정 리소스에 접근하려고 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트 애플리케이션은 사용자를 OAuth2 인증 서버로 리디렉션하여 로그인 및 권한 부여를 요청한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;사용자는 인증 서버에서 로그인하고, 특정 리소스에 대한 접근을 허용한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;인증 서버는 액세스 토큰(Access Token) 을 발급한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트 애플리케이션은 액세스 토큰을 사용하여 리소스 서버(Resource Server)에 요청을 보낸다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;리소스 서버는 액세스 토큰을 검증한 후, 유효한 경우 요청된 리소스를 반환한다.

------------------
### OAuth2와 기존 인증 방식 비교
OAuth2는 기존의 사용자 인증 방식(예: ID/PW 기반 로그인)과 비교했을 때 다음과 같은 차이점을 가진다.

비교 항목|기존 로그인 방식|OAuth2 방식
:---|:---|:---
보안성|비밀번호 노출 위험|토큰을 사용하여 보안 강화
유연성|특정 플랫폼에 종속|다양한 플랫폼에서 사용 가능
확장성|개별 애플리케이션마다 별도 관리 필요|단일 인증 서버를 통해 여러 애플리케이션에서 사용 가능
사용자 경험|서비스마다 별도 로그인 필요|소셜 로그인 등 통합 인증 가능

이러한 차이점 덕분에 OAuth2는 대규모 웹 서비스, API 기반 시스템, 모바일 애플리케이션 등에서 필수적인 인증 방식으로 자리 잡게 되었다.

-------------
### OAuth2의 실제 사용 사례
OAuth2는 다양한 서비스에서 사용되고 있으며, 대표적인 예로 다음과 같은 사례를 들 수 있다.

**소셜 로그인(Social Login)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Google, Facebook, Kakao, Naver 등의 계정을 이용하여 다른 애플리케이션에서 로그인할 수 있도록 한다.

**API 접근 제어**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GitHub API, Google Drive API, Twitter API 등은 OAuth2를 통해 인증된 사용자에게만 데이터를 제공한다.

**기업 내부 시스템 연동**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;사내 서비스 간 인증을 위해 OAuth2를 활용하여 싱글 사인온(SSO, Single Sign-On)을 구현할 수 있다.

--------------
## 1-2. OAuth2의 인증 방식
OAuth2는 다양한 환경에서 사용될 수 있도록 여러 가지 인증 방식을 제공한다. OAuth2의 인증 방식은 주어진 상황과 보안 요구 사항에 따라 선택될 수 있으며, 일반적으로 네 가지 인증 방식(Grant Type)이 사용된다.

### OAuth2 인증 방식이 필요한 이유
OAuth2의 인증 방식(Grant Type)은 다양한 클라이언트 유형과 환경에서 안전하게 권한을 위임할 수 있도록 설계되었다.<br>
예를 들어, 웹 애플리케이션과 모바일 애플리케이션은 보안 위험이 다르므로, 이에 맞는 인증 흐름이 필요하다. OAuth2의 인증 방식은 이러한 보안 요구 사항을 충족하면서도 사용자 경험을 해치지 않도록 설계되어 있다.

### Authorization Code Grant (인가 코드 방식)
이 방식은 가장 일반적으로 사용되는 OAuth2 인증 방식이다. 주로 웹 애플리케이션에서 사용되며, 클라이언트 애플리케이션이 직접 사용자 자격 증명을 처리하지 않고 인가 코드(Authorization Code) 를 이용하여 인증을 수행한다.

**동작 방식**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;사용자가 클라이언트 애플리케이션에서 로그인 요청을 한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트는 사용자를 OAuth2 인증 서버(Authorization Server) 로 리디렉션한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;사용자는 인증 서버에서 로그인하고, 인증 서버는 클라이언트에게 인가 코드를 발급한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트는 받은 인가 코드를 이용해 액세스 토큰(Access Token) 을 요청한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;인증 서버는 클라이언트의 요청을 검증한 후, 액세스 토큰을 발급한다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클라이언트는 액세스 토큰을 사용하여 리소스 서버에서 보호된 리소스를 요청한다.

**주요 특징**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;보안성이 높다: 인가 코드가 직접 사용자에게 전달되지 않고, 클라이언트와 인증 서버 간의 백엔드 통신을 통해 교환된다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;리프레시 토큰(Refresh Token) 지원: 사용자의 지속적인 인증이 필요할 경우, 새 액세스 토큰을 발급받을 수 있다.

예제 코드 (Spring Security 기반)
```java
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    http
        .authorizeHttpRequests(auth -> auth
            .requestMatchers("/private/**").authenticated()
            .anyRequest().permitAll()
        )
        .oauth2Login(Customizer.withDefaults()); // OAuth2 기반 로그인 활성화
    return http.build();
}
```
---------------
### Implicit Grant (암시적 승인 방식)
이 방식은 주로 SPA(Single Page Application) 같은 클라이언트 측 애플리케이션에서 사용되며, 인가 코드 없이 액세스 토큰을 직접 발급받는다.

동작 방식
사용자가 클라이언트 애플리케이션에서 로그인 요청을 한다.
클라이언트는 사용자를 인증 서버로 리디렉션한다.
사용자는 인증 서버에서 로그인하고, 액세스 토큰을 직접 전달받는다.
클라이언트는 액세스 토큰을 이용해 보호된 리소스에 접근한다.
주요 특징
보안성이 낮다: 액세스 토큰이 URL 프래그먼트(fragment)로 직접 전달되므로, 중간자 공격(MITM)에 취약할 수 있다.
리프레시 토큰 미지원: 보안 문제로 인해 리프레시 토큰이 지원되지 않으며, 토큰이 만료되면 다시 로그인해야 한다.
사용 제한
보안 문제로 인해 OAuth2.1에서는 제거되었으며, 권장되지 않는 방식이다.
대체 방식으로 PKCE(Proof Key for Code Exchange) 를 활용하는 것이 추천된다.
Resource Owner Password Credentials Grant (비밀번호 방식)
이 방식은 내부 시스템 또는 신뢰할 수 있는 애플리케이션에서 사용될 수 있다. 사용자가 애플리케이션에 직접 ID와 비밀번호를 입력하면, 클라이언트가 이를 이용해 액세스 토큰을 요청하는 방식이다.

동작 방식
사용자가 클라이언트 애플리케이션에서 ID와 비밀번호를 입력한다.
클라이언트는 이를 인증 서버에 전달하고, 액세스 토큰을 요청한다.
인증 서버는 사용자 정보를 검증한 후, 액세스 토큰을 발급한다.
클라이언트는 액세스 토큰을 이용해 보호된 리소스를 요청한다.
주요 특징
보안 위험이 있음: 클라이언트가 사용자 자격 증명을 직접 다루므로, 보안적으로 권장되지 않는다.
내부 서비스용으로 적합: 일반적인 사용자는 사용하지 않고, 내부 API 서비스에서 사용될 수 있다.
예제 코드 (Spring Security 기반)
@Bean
public AuthenticationManager authenticationManager(
        UserDetailsService userDetailsService,
        PasswordEncoder passwordEncoder) {
    DaoAuthenticationProvider authProvider = new DaoAuthenticationProvider();
    authProvider.setUserDetailsService(userDetailsService);
    authProvider.setPasswordEncoder(passwordEncoder);
    return new ProviderManager(authProvider);
}
Client Credentials Grant (클라이언트 자격 증명 방식)
이 방식은 사용자 없이 서버 간(API 서버 간) 인증이 필요한 경우 사용된다. 특정 클라이언트(애플리케이션)가 인증 서버에서 직접 액세스 토큰을 발급받아 리소스 서버와 통신하는 방식이다.

동작 방식
클라이언트가 인증 서버에 클라이언트 ID와 시크릿(Client Secret)을 전송하여 인증 요청을 한다.
인증 서버는 클라이언트를 검증하고, 액세스 토큰을 발급한다.
클라이언트는 발급받은 액세스 토큰을 이용하여 리소스 서버에 요청을 보낸다.
주요 특징
사용자가 개입하지 않음: 서버 간 통신에서 사용되므로, 사용자 로그인 과정이 필요하지 않다.
API 보안에 활용: 기업의 내부 API 또는 서비스 간 데이터 공유에 적합하다.
예제 코드 (Spring Security 기반)
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    http
        .authorizeHttpRequests(auth -> auth
            .requestMatchers("/api/**").authenticated()
            .anyRequest().permitAll()
        )
        .oauth2ResourceServer(OAuth2ResourceServerConfigurer::jwt);
    return http.build();
}
OAuth2 인증 방식 비교
인증 방식	사용 사례	보안 수준	특징
Authorization Code	웹 애플리케이션, 모바일 앱	높음	인가 코드 사용, 보안 강화
Implicit	SPA, 클라이언트 측 애플리케이션	낮음	액세스 토큰 직접 발급 (OAuth2.1에서 제거)
Password Grant	내부 시스템, 신뢰된 클라이언트	중간	사용자 자격 증명 필요, 권장되지 않음
Client Credentials	서버 간 API 인증	높음	사용자가 개입하지 않음
OAuth2 인증 방식은 애플리케이션의 특성과 보안 요구 사항에 따라 적절한 방식을 선택해야 한다. 특히, 보안 강화를 위해 Authorization Code 방식 + PKCE가 가장 권장되는 방식이다.

학습자의 사고를 돕기 위한 질문
Authorization Code Grant 방식이 보안적으로 가장 안전한 이유는 무엇인가?

Access Token이 클라이언트에 직접 노출되지 않는 구조를 떠올려보라.
Implicit Grant 방식이 점점 사용되지 않는 이유는 무엇인가?

클라이언트 측에서 Access Token을 직접 다루는 방식의 보안 취약점을 고려해보라.
1.3. OAuth2와 OpenID Connect (OIDC)
OAuth2는 애플리케이션이 사용자 정보를 안전하게 위임받아 사용할 수 있도록 설계된 권한 부여 프로토콜(Authorization Protocol) 이다. 그러나 OAuth2 자체는 사용자 인증(Authentication)을 담당하지 않으며, 대신 인증된 사용자의 권한을 위임하는 역할을 한다. 즉, OAuth2를 사용한다고 해서 애플리케이션이 사용자의 신원을 검증하는 것은 아니다.

이러한 OAuth2의 한계를 보완하기 위해 등장한 것이 OpenID Connect(OIDC) 이다. OIDC는 OAuth2를 기반으로 사용자 인증(Authentication) 기능을 추가하여, 애플리케이션이 신뢰할 수 있는 방식으로 사용자의 신원을 검증할 수 있도록 한다.

OpenID Connect(OIDC)의 개념
OpenID Connect(OIDC)는 OAuth2를 기반으로 사용자 인증(Authentication) 기능을 추가한 프로토콜이다. OAuth2가 "이 사용자에게 특정 리소스에 대한 접근 권한을 줄 수 있는가?"라는 질문을 해결하는 반면, OIDC는 "이 사용자가 실제로 누구인가?"라는 질문을 해결한다.

OIDC는 인증이 필요한 애플리케이션에서 OAuth2만으로는 부족한 사용자 인증 기능을 보완하여, 보다 신뢰할 수 있는 사용자 정보 제공 메커니즘을 제공한다.

OIDC는 다음과 같은 주요 기능을 포함한다.

ID Token 발급: 사용자의 신원을 검증하는 토큰을 제공한다.
OAuth2와의 통합: OAuth2를 기반으로 하기 때문에, 기존 OAuth2 인증 흐름과 쉽게 결합할 수 있다.
확장성: OIDC는 다양한 애플리케이션 환경(웹, 모바일, 데스크톱 등)에서 동작할 수 있도록 설계되었다.
OAuth2와 OpenID Connect의 차이점
기능	OAuth2	OpenID Connect (OIDC)
목적	권한 부여 (Authorization)	사용자 인증 (Authentication)
주요 역할	리소스에 대한 액세스 권한 부여	사용자의 신원을 검증하고 정보 제공
Access Token 포함 여부	포함	포함 (보안 강화를 위해 추가)
ID Token 제공 여부	없음	있음 (사용자의 정보를 포함)
사용 사례	API 보호, 애플리케이션 간 권한 위임	소셜 로그인, SSO(Single Sign-On) 등
표준화 여부	보안 요구 사항이 명확하지 않음	표준화된 인증 프로세스 제공
OAuth2만 사용할 경우, 애플리케이션이 사용자의 신원을 직접 검증할 방법이 없다. 반면, OpenID Connect는 OAuth2의 인증 서버가 사용자 정보를 포함한 ID Token을 발급하여, 애플리케이션이 해당 사용자가 실제 누구인지 확인할 수 있도록 한다.

ID Token이란?
ID Token은 OpenID Connect에서 사용자의 신원을 검증하기 위해 발급되는 JWT(JSON Web Token) 형태의 토큰이다. Access Token이 API 리소스 접근을 위한 권한을 부여하는 데 사용된다면, ID Token은 사용자의 신원을 증명하는 역할을 한다.

ID Token의 구조는 일반적인 JWT와 동일하며, 다음과 같은 세 부분으로 구성된다.

Header (헤더)

토큰의 서명 방식(HMAC, RSA 등)을 지정한다.
Payload (페이로드)

사용자의 정보(클레임, Claims)를 포함한다.
일반적으로 sub(사용자 ID), iss(발급자), exp(만료 시간) 등이 포함된다.
Signature (서명)

토큰의 무결성을 검증하기 위한 서명이 포함된다.
예제: ID Token의 구조 (JWT 형태)
{
  "alg": "RS256",
  "typ": "JWT"
}
.
{
  "sub": "1234567890",
  "name": "John Doe",
  "email": "john.doe@example.com",
  "iss": "https://auth.example.com",
  "aud": "client-id-123",
  "exp": 1716239022
}
.
"HMACSHA256(Base64UrlEncode(header) + '.' + Base64UrlEncode(payload), secret)"
OIDC 인증 흐름 (Authorization Code Flow)
OIDC는 OAuth2의 Authorization Code Flow를 기반으로 인증을 수행한다. 기본적인 흐름은 다음과 같다.

사용자가 애플리케이션에 로그인 요청
→ 클라이언트 애플리케이션(예: 웹 앱, 모바일 앱)이 사용자를 로그인 페이지로 리디렉션한다.

사용자는 인증 서버에서 로그인
→ OAuth2 인증 서버가 사용자 자격 증명을 확인하고 인증을 진행한다.

인증 서버가 Authorization Code 반환
→ 로그인 성공 시, 클라이언트 애플리케이션은 Authorization Code를 발급받는다.

클라이언트 애플리케이션이 Authorization Code를 사용해 토큰 요청
→ 클라이언트는 받은 Authorization Code를 사용하여 인증 서버에 Access Token과 ID Token을 요청한다.

Access Token과 ID Token 발급
→ 인증 서버는 Access Token과 ID Token을 클라이언트 애플리케이션에 반환한다.

클라이언트 애플리케이션이 ID Token을 검증하여 사용자 정보 확인
→ 클라이언트 애플리케이션은 ID Token을 디코딩하여, 사용자의 신원을 확인하고 로그인 세션을 생성한다.

OIDC 인증 요청 예제 (Authorization Code Flow)
GET /authorize?
   response_type=code
   &client_id=client-id-123
   &redirect_uri=https://example.com/callback
   &scope=openid profile email
   &state=xyz123
   &nonce=nonce-value
   &code_challenge=code-challenge
   &code_challenge_method=S256
   HTTP/1.1
Host: auth.example.com
이후 클라이언트는 Authorization Code를 받아 다음과 같이 Access Token과 ID Token을 요청할 수 있다.

토큰 요청 예제
POST /token HTTP/1.1
Host: auth.example.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code
&code=authorization-code-value
&redirect_uri=https://example.com/callback
&client_id=client-id-123
&client_secret=client-secret
&code_verifier=code-verifier-value
OpenID Connect의 활용 사례
OIDC는 다양한 환경에서 사용될 수 있으며, 다음과 같은 주요 활용 사례가 있다.

소셜 로그인 (Social Login)

Google, Facebook, Naver, Kakao 등의 OAuth2 Provider를 이용하여 간편 로그인 기능을 구현할 수 있다.
SSO (Single Sign-On)

한 번 로그인하면 여러 서비스에서 동일한 사용자 인증 정보를 사용할 수 있도록 한다.
기업 내부 시스템의 인증

사내 애플리케이션에서 OIDC 기반의 인증 시스템을 구축할 수 있다.
API 및 마이크로서비스 보안 강화

OAuth2의 권한 위임과 OIDC의 사용자 인증을 조합하여 보다 강력한 보안 구조를 만들 수 있다.
학습자의 사고를 돕기 위한 질문
OAuth2는 인증(Authentication) 프로토콜이 아닌 이유는 무엇인가?

OAuth2의 목적이 무엇인지 다시 떠올려보라.
OpenID Connect(OIDC)가 OAuth2와 함께 사용될 때 제공하는 추가적인 기능은 무엇인가?

ID Token과 사용자 프로필 정보의 역할을 생각해보라.
2. JWT(Json Web Token) 개요
2.1. JWT의 개념
JWT(Json Web Token)는 인증과 정보 교환을 위해 사용되는 JSON 기반의 토큰이다. JWT는 서버와 클라이언트 간의 상태를 유지하지 않는(stateless) 인증 방식을 가능하게 하며, 인증된 정보를 안전하게 전달하는 역할을 한다.

기존의 세션 기반 인증(Session-based Authentication) 에서는 클라이언트가 로그인하면, 서버는 해당 클라이언트의 세션 정보를 저장하고 이를 관리해야 한다. 하지만 JWT 기반 인증(Token-based Authentication) 에서는 클라이언트가 로그인할 때, 서버는 특정 정보를 포함한 JWT를 발급하고, 이후 클라이언트가 이 토큰을 요청마다 포함하여 서버에 전달하면 된다. 이 방식은 서버가 세션을 직접 관리할 필요가 없기 때문에, 확장성(Scalability)이 뛰어나다.

JWT의 주요 특징
토큰 기반 인증(Token-based Authentication)

JWT는 인증 정보를 포함한 토큰을 발급하여, 별도의 세션을 유지할 필요 없이 사용자 인증을 처리할 수 있다.
클라이언트는 서버에서 받은 JWT를 API 요청마다 포함하여 보냄으로써 인증을 유지한다.
JSON 기반의 데이터 구조

JWT는 JSON 형태로 인코딩되며, 클라이언트와 서버 간 쉽게 데이터를 주고받을 수 있다.
경량(Lightweight)하며, 다양한 프로그래밍 언어에서 쉽게 활용할 수 있다.
자체 포함(Self-contained)

JWT 내부에 필요한 정보를 모두 포함하고 있어, 별도의 데이터베이스 조회 없이도 토큰만으로 사용자 인증을 수행할 수 있다.
예를 들어, 사용자의 권한(Role) 정보를 포함할 수도 있다.
무결성 보장

JWT는 디지털 서명(Digital Signature) 을 포함하기 때문에 변조가 어렵다.
서버는 클라이언트가 보낸 JWT가 조작되지 않았음을 서명을 검증하는 방식으로 확인할 수 있다.
확장성(Scalability) 우수

세션 저장이 필요 없는 구조이므로, 분산 시스템(Distributed System) 환경에서 효과적이다.
클라이언트가 토큰을 보유하고 있으므로, 요청이 증가해도 서버의 부하가 상대적으로 낮다.
JWT의 구조
JWT는 세 개의 구성 요소(Header, Payload, Signature) 로 이루어져 있으며, 각 요소는 마침표(.)로 구분된다.

<Header>.<Payload>.<Signature>
이러한 구조를 통해 JWT는 변조 방지 기능을 제공하면서도, 클라이언트가 필요한 정보를 포함할 수 있도록 설계되었다.

JWT 예제 (Base64 인코딩된 형태)
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
.
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvbiBEb2UiLCJpYXQiOjE1MTYyMzkwMjJ9
.
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
각 구성 요소를 하나씩 살펴보면 다음과 같다.

1. Header (헤더)
JWT의 헤더(Header) 는 토큰의 타입과 서명 알고리즘을 지정하는 JSON 객체이다. JWT를 사용할 때, 어떤 방식으로 서명되었는지를 확인하는 역할을 한다.

Header 예제 (JSON 형태)
{
  "alg": "HS256",
  "typ": "JWT"
}
alg (Algorithm) : 서명에 사용할 알고리즘을 명시 (HS256, RS256, ES256 등).
typ (Type) : 토큰 타입을 명시 (JWT).
해당 JSON 객체는 Base64Url 인코딩을 거쳐 JWT의 첫 번째 부분을 구성한다.

2. Payload (페이로드)
Payload(페이로드) 는 JWT의 본문으로, 인증과 관련된 클레임(Claim) 정보를 포함한다.

Payload 예제 (JSON 형태)
{
  "sub": "1234567890",
  "name": "John Doe",
  "iat": 1516239022,
  "exp": 1516249022
}
sub (Subject) : 토큰의 주체(사용자 ID).
name: 사용자 이름.
iat (Issued At) : 토큰 발급 시간.
exp (Expiration Time) : 토큰 만료 시간.
Payload는 또한 사용자 정의 데이터를 포함할 수도 있으며, 일반적으로 토큰의 유효 기간(exp), 발급자(iss), 사용자 권한(role) 등의 정보가 포함된다.

이 JSON 객체도 Base64Url 인코딩을 거쳐 JWT의 두 번째 부분을 구성한다.

3. Signature (서명)
서명(Signature) 은 JWT의 무결성을 보장하기 위해 사용된다.
서명은 헤더(Header)와 페이로드(Payload)를 조합한 후, 특정 비밀 키를 사용해 생성된다.

서명 생성 방식 (HMAC SHA256)
HMACSHA256(
  base64UrlEncode(Header) + "." +
  base64UrlEncode(Payload),
  secret
)
이렇게 생성된 서명은 JWT의 마지막 부분을 구성하며, 토큰이 변조되지 않았음을 서버가 검증하는 데 사용된다.

JWT 예제 (전체 구조)
아래는 실제 JWT를 구성하는 예제이다.

JWT 예제 (Base64Url 인코딩)
Header:
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9

Payload:
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvbiBEb2UiLCJpYXQiOjE1MTYyMzkwMjJ9

Signature:
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
JWT는 이처럼 Header, Payload, Signature 세 가지 요소로 구성되며, 토큰 내부에 정보를 포함하여 상태를 유지하지 않는 인증 방식을 가능하게 한다.

JWT의 활용 사례
JWT는 다양한 환경에서 활용될 수 있으며, 대표적인 사례는 다음과 같다.

사용자 인증(Authentication)

사용자가 로그인하면, 서버는 JWT를 발급하여 클라이언트가 이후 요청마다 이를 포함하도록 한다.
예를 들어, 웹 애플리케이션에서 로그인 후 세션을 사용하지 않고 JWT로 인증을 유지할 수 있다.
API 접근 권한 관리(Authorization)

클라이언트는 API 요청을 보낼 때, JWT를 HTTP 헤더에 포함하여 서버에 인증 정보를 제공할 수 있다.
예제:
GET /api/user/profile HTTP/1.1
Host: example.com
Authorization: Bearer <JWT>
싱글 사인온(SSO, Single Sign-On)

여러 애플리케이션에서 한 번의 로그인으로 사용자를 인증할 수 있도록 JWT를 활용할 수 있다.
정보 보호 및 무결성 유지

JWT는 서명(Signature)을 포함하여 변조를 방지할 수 있다.
학습자의 사고를 돕기 위한 질문
JWT는 왜 JSON 형식을 사용하여 정보를 저장하는가?

데이터 교환의 용이성과 구조적 접근성을 고려해보라.
JWT가 일반적인 세션 기반 인증 방식과 비교했을 때 가지는 장점은 무엇인가?

상태를 유지하지 않는(stateless) 방식의 특징을 떠올려보라.
2.2. JWT의 동작 방식
JWT(Json Web Token)는 클라이언트와 서버 간의 인증 및 권한 부여를 위한 중요한 토큰 기반 인증 방식이다. 이를 이해하기 위해 JWT가 생성되고 검증되는 과정을 단계별로 살펴보자.

JWT 발급 및 인증 흐름
JWT는 사용자의 인증을 위해 발급되며, 이후 API 요청에서 사용된다. 다음은 JWT 인증 과정을 단계별로 설명한 것이다.

사용자가 로그인 요청

사용자는 아이디와 비밀번호를 입력하여 로그인 요청을 보낸다.
서버는 해당 사용자의 자격 증명을 검증한다.
서버에서 JWT 발급

로그인에 성공하면, 서버는 사용자의 정보를 포함한 JWT를 생성한다.
JWT에는 사용자의 ID, 권한(Role) 정보, 발급 시간(iat), 만료 시간(exp) 등의 정보가 포함될 수 있다.
서버는 이 JWT를 클라이언트에게 반환한다.
클라이언트에서 JWT 저장

클라이언트(예: 웹 브라우저, 모바일 앱)는 발급된 JWT를 저장한다.
일반적으로 JWT는 다음과 같은 방식으로 저장될 수 있다.
로컬 스토리지(LocalStorage) : 브라우저에서 localStorage.setItem("token", JWT) 형태로 저장.
세션 스토리지(SessionStorage) : 세션 종료 시 삭제되는 방식으로 저장.
HTTP 쿠키(HTTP-Only Cookie) : XSS 공격 방지를 위해 보안 설정된 쿠키에 저장.
클라이언트가 API 요청 시 JWT 포함

이후 클라이언트가 API를 호출할 때, 요청 헤더에 JWT를 포함한다.
일반적으로 Authorization 헤더에 Bearer 토큰 방식으로 전송된다.
GET /api/user/profile HTTP/1.1
Host: example.com
Authorization: Bearer <JWT>
서버에서 JWT 검증

서버는 요청을 받으면, Authorization 헤더에서 JWT를 추출한다.
서버는 JWT의 서명을 검증하여 변조되지 않았음을 확인한다.
만약 JWT가 유효하다면, 해당 사용자의 정보로 요청을 처리한다.
API 응답 반환

서버는 JWT 검증이 완료되면, 요청에 대한 적절한 응답을 클라이언트에 반환한다.
클라이언트는 응답을 받아 화면에 데이터를 표시하거나 다음 작업을 수행한다.
JWT 인증 흐름 예제
아래는 JWT를 활용한 인증 과정에서의 클라이언트-서버 상호작용을 보여주는 예제이다.

1. 클라이언트에서 로그인 요청 (사용자 로그인)
POST /auth/login HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "username": "user1",
  "password": "password123"
}
2. 서버에서 JWT 발급 후 응답
HTTP/1.1 200 OK
Content-Type: application/json

{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
3. 클라이언트가 API 요청 시 JWT 포함
GET /api/user/profile HTTP/1.1
Host: example.com
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
4. 서버에서 JWT 검증 후 응답
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "username": "user1",
  "email": "user1@example.com"
}
JWT 서명 방식
JWT의 보안성을 높이기 위해 서명이 사용된다. 서버는 JWT를 생성할 때 비밀 키(Secret Key) 또는 공개-개인 키(Public-Private Key) 쌍을 이용하여 서명한다.

HMAC (HMAC-SHA256)

대칭 키 방식의 서명 알고리즘.
서버에서만 비밀 키를 알고 있어야 하며, 해당 키를 이용해 토큰이 변조되지 않았는지 검증할 수 있다.
RSA (RS256, RS512)

비대칭 키 방식의 서명 알고리즘.
서버는 개인 키(Private Key)로 서명하고, 공개 키(Public Key)로 검증할 수 있다.
JWT 서명 예제 (HMAC SHA256 방식)
HMACSHA256(
  base64UrlEncode(Header) + "." +
  base64UrlEncode(Payload),
  secret
)
위와 같은 방식으로 서명이 생성되며, 서버는 요청을 받을 때마다 서명이 변조되지 않았는지 검증한다.

JWT 검증 과정
서버는 클라이언트가 보낸 JWT를 검증하여 유효한지 확인해야 한다. 검증 과정에서 다음을 체크한다.

토큰의 서명이 유효한지 확인

클라이언트가 보낸 JWT의 서명을 서버에서 검증한다.
서명이 유효하지 않으면 토큰이 변조되었을 가능성이 높다.
토큰의 만료 시간(exp) 확인

JWT는 exp(Expiration) 필드에 만료 시간이 포함될 수 있다.
만료된 JWT는 유효하지 않으며, 새 토큰을 발급해야 한다.
토큰의 발급자(iss) 및 대상(aud) 확인

iss(Issuer) 필드는 토큰을 발급한 서버를 나타낸다.
aud(Audience) 필드는 해당 토큰이 특정 서비스에서만 사용 가능하도록 지정한다.
JWT 검증 코드 예제 (Java Spring Boot)
Spring Security를 사용하여 JWT를 검증하는 코드 예제는 다음과 같다.

import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;

import java.util.Date;

public class JwtUtil {
    private static final String SECRET_KEY = "mySecretKey";

    // JWT 생성
    public static String generateToken(String username) {
        return Jwts.builder()
                .setSubject(username)
                .setIssuedAt(new Date())
                .setExpiration(new Date(System.currentTimeMillis() + 1000 * 60 * 60)) // 1시간 유효
                .signWith(SignatureAlgorithm.HS256, SECRET_KEY)
                .compact();
    }

    // JWT 검증
    public static Claims verifyToken(String token) {
        return Jwts.parser()
                .setSigningKey(SECRET_KEY)
                .parseClaimsJws(token)
                .getBody();
    }
}
위 코드에서 generateToken 메서드는 JWT를 생성하며, verifyToken 메서드는 토큰을 검증한다.

JWT의 특징 요약
클라이언트와 서버 간 상태를 유지하지 않는(stateless) 방식으로 인증이 가능하다.
JWT는 헤더(Header), 페이로드(Payload), 서명(Signature)로 구성된다.
API 요청 시 Authorization: Bearer <JWT> 형식으로 토큰을 포함하여 인증을 수행한다.
서버는 JWT의 서명을 검증하여 토큰이 변조되지 않았음을 확인한다.
토큰의 유효 기간을 설정하여 보안성을 높일 수 있다.
학습자의 사고를 돕기 위한 질문
JWT가 서버에서 사용자의 인증 정보를 검증할 때 데이터베이스 조회 없이도 검증할 수 있는 이유는 무엇인가?

JWT의 서명(Signature) 검증 방식과 토큰 자체에 정보를 포함하는 특징을 고려해보라.
JWT가 클라이언트-서버 간의 인증 과정에서 일반적인 쿠키-세션 방식보다 효율적인 경우는 언제인가?

분산 시스템이나 마이크로서비스 환경을 고려해보라.
실습 문제
문제 1: JWT의 구조 분석
다음 요구사항을 만족하는 코드를 작성하시오.

JWT를 구성하는 3개의 주요 요소(Header, Payload, Signature)를 개별적으로 출력한다.
예제 토큰(eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...)을 디코딩하여, Payload에 담긴 정보를 확인한다.
Header와 Payload는 Base64 디코딩을 활용하여 분석한다.
문제 2: JWT 발급과 검증 흐름 이해
다음 요구사항을 만족하는 코드를 작성하시오.

사용자의 ID와 역할(Role)을 포함하는 JWT를 생성한다.
생성된 JWT를 검증하여 유효한 토큰인지 확인한다.
토큰이 유효한 경우 Payload 정보를 출력한다.
2.3. JWT의 장점과 보안 고려 사항
JWT는 클라이언트와 서버 간의 인증 및 권한 부여를 위해 사용되며, 세션을 유지하지 않아도 되는(stateless) 구조와 빠른 인증 속도 등의 장점이 있다. 하지만, JWT를 안전하게 사용하기 위해서는 보안 취약점을 고려해야 한다. 이번 장에서는 JWT의 주요 장점과 보안 고려 사항을 설명한다.

JWT의 주요 장점
JWT가 널리 사용되는 이유는 다음과 같은 핵심적인 장점 때문이다.

Stateless(상태 유지가 필요 없음)

JWT는 클라이언트 측에서 보관되며, 요청마다 JWT를 서버로 보내 검증하는 방식이다.
서버가 사용자의 인증 상태를 저장할 필요가 없으므로, 세션(session) 기반 인증보다 확장성이 뛰어나다.
서버 간 로드 밸런싱(Load Balancing) 환경에서 효과적으로 사용 가능하다.
빠른 인증 처리

JWT는 단순한 문자열 기반의 토큰이므로, 서버가 데이터베이스(DB)에 접근하여 인증 정보를 조회할 필요가 없다.
대신, 서버는 JWT의 서명(Signature) 을 검증하는 것만으로 사용자를 인증할 수 있어 응답 속도가 빠르다.
다양한 플랫폼 및 프로토콜 지원

JSON 형식의 데이터 구조를 사용하기 때문에 모든 프로그래밍 언어에서 쉽게 파싱(Parsing) 가능하다.
RESTful API, GraphQL, WebSocket 등 다양한 통신 방식에서 인증을 지원한다.
클라이언트에서 자체적으로 정보 활용 가능

JWT의 Payload(페이로드) 에 포함된 정보를 디코딩(Decoding)하면, 사용자 ID, 권한(Role) 등의 정보를 읽을 수 있다.
별도의 API 요청 없이 클라이언트 측에서 사용자의 권한을 확인하는 데 활용할 수 있다.
하지만, Payload 데이터는 서명(Signature)만 보호되고 암호화되지 않기 때문에 중요한 정보는 포함하지 않는 것이 좋다.
Access Token과 Refresh Token의 분리 가능

JWT 기반 인증에서는 Access Token(짧은 수명) 과 Refresh Token(긴 수명) 을 별도로 발급하여 보안성과 인증 편의성을 동시에 제공할 수 있다.
Access Token은 짧은 시간만 유효하도록 설정하고, Refresh Token을 활용하여 새로운 Access Token을 발급받는 방식이 가능하다.
JWT 사용 시 보안 고려 사항
JWT는 위와 같은 장점을 가지고 있지만, 보안 설정을 적절히 하지 않으면 심각한 보안 문제가 발생할 수 있다. 따라서, JWT 사용 시 고려해야 할 보안 요소들을 살펴보자.

HTTPS를 통한 안전한 전송

JWT는 요청 헤더(Authorization: Bearer <토큰>)에 포함되어 전송된다.
평문 HTTP 환경에서는 JWT가 탈취될 위험이 크므로, 반드시 HTTPS를 사용해야 한다.
HTTPS를 사용하지 않는 경우, 중간자 공격(Man-in-the-Middle, MITM) 에 취약할 수 있다.
토큰 만료 시간(exp) 설정

JWT는 발급 후 유효 기간이 설정되지 않으면, 만료되지 않고 계속 사용될 위험이 있다.
exp(Expiration) 클레임을 설정하여, 일정 시간이 지나면 토큰이 만료되도록 해야 한다.
보통 Access Token의 만료 시간은 짧게(예: 15분 ~ 1시간) , Refresh Token의 만료 시간은 길게(예: 7일 ~ 30일) 설정하는 것이 일반적이다.
{
  "exp": 1712710800  // UNIX Timestamp (만료 시간)
}
JWT 서명(Signature)의 강력한 보안 유지

JWT의 무결성을 보장하기 위해 서명(Signature)을 사용하지만, 서명 키(Secret Key)가 노출되면 누구나 JWT를 위조할 수 있다.
따라서, 비밀 키(Secret Key)는 서버에서 환경 변수(.env 파일) 또는 보안 저장소에 안전하게 저장해야 한다.
대칭 키(HMAC)보다는 비대칭 키(RSA, ECDSA) 방식을 사용하는 것이 더 안전하다.
JWT 저장 위치 및 보안

클라이언트에서 JWT를 저장할 때, 로컬 스토리지(LocalStorage)나 세션 스토리지(SessionStorage)를 사용하는 것은 보안적으로 취약하다.
쿠키(Cookie) + HTTP-Only 설정을 사용하면, JavaScript에서 접근할 수 없도록 하여 XSS(크로스 사이트 스크립팅) 공격을 방지할 수 있다.
// Spring Boot - JWT 쿠키 설정
ResponseCookie jwtCookie = ResponseCookie.from("token", jwt)
    .httpOnly(true)  // XSS 공격 방지
    .secure(true)    // HTTPS에서만 사용
    .path("/")
    .maxAge(60 * 60) // 1시간 유지
    .build();
response.addHeader(HttpHeaders.SET_COOKIE, jwtCookie.toString());
토큰 재사용 방지 및 블랙리스트 관리

JWT는 기본적으로 상태를 유지하지 않기 때문에, 사용자가 로그아웃을 해도 기존 토큰이 유효한 상태로 남아있을 수 있다.
이를 방지하기 위해, 서버에서 로그아웃한 사용자의 JWT를 블랙리스트에 등록하여 차단할 수 있다.
또는, 토큰이 요청될 때마다 기존 토큰과 비교하는 데이터베이스 검증 방식을 적용할 수 있다.
JWT Payload 데이터 보호

JWT의 Payload에는 사용자 정보(예: userId, role, email 등)를 포함할 수 있지만, 이는 단순한 Base64 URL Encoding 방식으로 인코딩된 것이므로 누구나 디코딩이 가능하다.
따라서, 중요한 데이터(예: 비밀번호, 카드 정보)는 절대로 Payload에 포함해서는 안 된다.
중요한 데이터가 필요할 경우, JWT의 JWE(JSON Web Encryption) 암호화 방식을 사용하거나, 해당 데이터를 서버에서 관리하는 것이 안전하다.
JWT의 길이 제한 및 최적화

JWT는 일반적으로 Header, Payload, Signature를 포함한 문자열로 구성되며, 길이가 길어질 수 있다.
Payload에 불필요한 정보를 포함하면, 토큰의 크기가 커져 전송 속도에 영향을 줄 수 있다.
따라서, 최소한의 정보만 포함하도록 설계하고, 필요할 경우 토큰을 압축하는 방안을 고려해야 한다.
보안 설정을 반영한 JWT 예제 (Spring Boot)
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import java.util.Date;

public class JwtUtil {
    private static final String SECRET_KEY = "SuperSecureSecretKey123!"; // 외부 환경변수로 관리해야 함

    // JWT 생성
    public static String generateToken(String username) {
        return Jwts.builder()
                .setSubject(username)
                .setIssuedAt(new Date()) // 토큰 발급 시간
                .setExpiration(new Date(System.currentTimeMillis() + 1000 * 60 * 15)) // 15분 후 만료
                .signWith(SignatureAlgorithm.HS256, SECRET_KEY) // HMAC-SHA256 서명
                .compact();
    }

    // JWT 검증
    public static boolean validateToken(String token) {
        try {
            Jwts.parser()
                .setSigningKey(SECRET_KEY)
                .parseClaimsJws(token);
            return true; // 검증 성공
        } catch (Exception e) {
            return false; // 검증 실패
        }
    }
}
학습자의 사고를 돕기 위한 질문
JWT의 stateless 특성이 인증 시스템에서 어떤 이점을 제공하는가?

중앙 서버에 세션을 저장하지 않는 구조를 고려해보라.
JWT를 사용할 때 보안적으로 고려해야 할 주요 사항은 무엇인가?

토큰 탈취, 만료 시간, 서명 검증 등의 보안 요소를 떠올려보라.
3. OAuth2와 JWT의 관계 및 통합 개념
3.1. OAuth2에서 JWT를 사용하는 이유
OAuth2는 애플리케이션이 사용자 인증 및 권한 부여를 위임받을 수 있도록 설계된 프로토콜이다. 그러나 OAuth2 자체는 액세스 토큰의 형식을 명확히 정의하지 않는다. 즉, OAuth2의 액세스 토큰은 반드시 특정 포맷을 따라야 하는 것이 아니라 다양한 형태로 구현될 수 있다. 여기서 JWT(Json Web Token) 를 액세스 토큰으로 활용하면 여러 가지 이점이 존재하며, 특히 OAuth2 기반 API 인증에서 큰 강점을 발휘한다.

이번 장에서는 OAuth2에서 JWT를 사용하는 이유를 설명하고, JWT가 OAuth2 기반 인증에서 어떻게 활용될 수 있는지에 대해 자세히 다룬다.

OAuth2의 기존 액세스 토큰 방식
OAuth2에서 액세스 토큰은 기본적으로 문자열 형태의 토큰으로 발급된다. 즉, 서버가 랜덤한 문자열을 생성하여 액세스 토큰을 발급하고, 해당 토큰을 이용해 클라이언트가 API를 호출하는 방식이다. 이런 방식에서는 일반적으로 액세스 토큰을 데이터베이스(DB)에서 관리하게 되며, 클라이언트가 토큰을 전송하면 서버가 이를 조회하여 인증 여부를 확인하는 구조를 가진다.

그러나, 이러한 방식은 몇 가지 문제를 유발할 수 있다.

토큰 검증 시 성능 저하

액세스 토큰을 검증하려면 서버가 DB에서 해당 토큰을 조회하는 과정이 필요하다.
트래픽이 많아질수록 DB 조회 부담이 커지며, API 요청에 대한 응답 시간이 증가할 수 있다.
확장성 문제

서버가 액세스 토큰을 중앙에서 관리하므로, 여러 개의 서버가 있는 환경에서 토큰을 공유하기 어렵다.
하나의 서버에서 발급된 토큰을 다른 서버에서 검증하려면, 공유 저장소나 별도의 인증 서버를 구축해야 하는 복잡성이 추가된다.
보안 문제

토큰이 탈취되면, 악의적인 사용자가 서버의 DB에 저장된 유효한 토큰을 계속 사용할 가능성이 있다.
특정 토큰을 무효화하려면 블랙리스트(Blacklist) 관리가 필요하며, 이는 추가적인 DB 연산을 요구한다.
OAuth2에서 JWT를 사용하면 해결할 수 있는 문제
OAuth2의 액세스 토큰을 JWT 기반으로 발급하면 앞서 설명한 문제를 해결할 수 있다.

토큰 검증 시 DB 조회 불필요 (Stateless)

JWT는 디지털 서명을 포함하는 자체 포함(Self-contained) 토큰이다.
서버는 토큰을 DB에서 조회하지 않고 서명(Signature)만 검증하여 즉시 신뢰할 수 있는 데이터인지 판단할 수 있다.
즉, API 요청 시마다 DB 조회가 필요하지 않아 성능이 크게 향상된다.
토큰 공유 및 확장성 향상

JWT는 서버 간에 공유할 수 있는 토큰이므로, 여러 개의 API 서버에서 같은 JWT를 검증할 수 있다.
이를 통해 OAuth2 기반의 분산 시스템에서 인증 서버를 따로 두지 않아도 된다.
유효 기간이 포함된 보안 강화

JWT에는 토큰 만료 시간(exp, expiration time)이 포함되어 있어, 클라이언트가 만료된 토큰을 사용하지 않도록 자동으로 제한할 수 있다.
일반적인 OAuth2 토큰에서는 DB에서 만료 여부를 체크해야 하지만, JWT는 자체적으로 만료 시간을 검증할 수 있다.
추가적인 사용자 정보 포함 가능

일반적인 OAuth2 토큰은 단순한 문자열이므로, 토큰만으로 사용자 정보를 확인할 수 없다.
반면, JWT의 Payload에는 사용자 ID, 권한(Role), 이메일 등 다양한 정보를 포함할 수 있다.
이를 통해 추가적인 DB 조회 없이도 사용자 정보를 활용할 수 있다.
JWT를 사용한 OAuth2 액세스 토큰 예제
OAuth2에서 JWT를 액세스 토큰으로 활용하면, JWT의 Payload에 사용자 관련 정보를 담아서 API 인증을 간편하게 수행할 수 있다. 일반적인 JWT 액세스 토큰의 예시는 다음과 같다.

{
  "iss": "auth.server.com",  // 발급자(Authorization Server)
  "sub": "user123",         // 사용자 ID
  "aud": "myapi.com",       // 대상 API 서버
  "exp": 1712710800,        // 만료 시간(UNIX Timestamp)
  "iat": 1712707200,        // 발급 시간
  "scope": "read write",    // 권한 범위(Scope)
  "role": "USER"            // 사용자 역할(Role)
}
위와 같은 JWT 구조를 사용하면, 별도의 DB 조회 없이도 사용자의 ID, 권한, 만료 여부를 즉시 확인할 수 있다. 서버는 클라이언트로부터 JWT를 전달받은 후, 서명을 검증하여 해당 토큰이 신뢰할 수 있는지 확인하면 된다.

JWT 기반 OAuth2 인증 흐름
OAuth2에서 JWT를 액세스 토큰으로 사용하는 인증 흐름은 다음과 같다.

사용자가 로그인 요청

사용자가 OAuth2 클라이언트를 통해 로그인한다.
OAuth2 Authorization Server에서 JWT 발급

인증 서버(Authorization Server)는 사용자의 정보를 확인한 후, JWT 형식의 액세스 토큰을 생성하여 클라이언트에 반환한다.
클라이언트가 API 호출 시 JWT 포함

클라이언트는 API를 호출할 때 Authorization: Bearer <JWT> 헤더를 포함하여 요청을 보낸다.
Resource Server에서 JWT 검증

API 서버(Resource Server)는 전달받은 JWT를 검증하여, 사용자가 유효한지, 권한이 적절한지 판단한 후 API 요청을 처리한다.
JWT를 사용한 OAuth2 인증의 한계점
JWT는 OAuth2 액세스 토큰으로 사용하기에 많은 장점을 제공하지만, 몇 가지 고려해야 할 사항도 있다.

JWT는 한 번 발급되면 변경할 수 없다

JWT는 자체 포함된 토큰이므로, 한 번 발급된 후에는 서버에서 해당 JWT를 무효화할 방법이 없다.
즉, 사용자가 로그아웃을 해도 기존 JWT는 만료될 때까지 여전히 유효할 수 있다.
이를 해결하기 위해 짧은 만료 시간(exp)을 설정하고, Refresh Token을 활용하는 방식을 사용한다.
서명 검증이 필요하므로 약간의 연산 비용이 존재

JWT 검증 과정에서 서명(Signature)을 확인하는 연산이 필요하므로, 단순한 문자열 기반 토큰보다 약간의 CPU 연산이 추가된다.
그러나, 이는 DB 조회 비용보다 훨씬 낮은 비용으로 유지할 수 있다.
Payload 데이터는 암호화되지 않는다

JWT의 Payload는 Base64 URL 인코딩된 값이므로, 누구나 디코딩하여 내용을 확인할 수 있다.
따라서, 중요한 정보(예: 비밀번호, 카드 정보)를 JWT에 포함하지 않도록 주의해야 한다.
중요한 데이터가 필요할 경우, JWT 대신 JWE(JSON Web Encryption)를 활용하여 암호화된 토큰을 사용하는 방식을 고려해야 한다.
학습자의 사고를 돕기 위한 질문
OAuth2는 원래 자체적인 인증 방식(예: Authorization Code Grant)을 제공하는데, 왜 JWT를 사용하여 인증을 보완하는가?

OAuth2의 인증 프로세스와 JWT의 stateless 특성을 비교해보라.
JWT를 OAuth2의 Access Token으로 활용할 경우, 기존의 OAuth2 토큰 방식과 비교했을 때 어떤 장점이 있는가?

토큰의 검증 방식과 네트워크 요청의 감소 여부를 고려해보라.
3.2. OAuth2 기반 JWT 인증 흐름
OAuth2와 JWT를 결합하면 인증 및 권한 부여 과정이 단순해지고 확장성이 커진다. 특히, OAuth2 인증 서버에서 JWT 기반 액세스 토큰을 발급하면 리소스 서버가 별도의 DB 조회 없이 토큰을 검증하고 요청을 처리할 수 있다. 이를 통해 인증 속도가 향상되며, 분산 시스템에서 중앙 인증 서버의 부하를 줄일 수 있다.

이번 장에서는 OAuth2에서 JWT를 활용한 인증 흐름을 구체적으로 설명하며, 각 단계에서의 역할을 분석한다.

OAuth2에서 JWT 기반 인증 흐름 개요
OAuth2 인증 과정에서 JWT를 활용하면, 다음과 같은 흐름으로 인증이 이루어진다.

사용자가 클라이언트를 통해 로그인 요청을 보낸다.
클라이언트는 OAuth2 인증 서버로부터 JWT 액세스 토큰을 요청한다.
OAuth2 인증 서버는 사용자 정보를 확인한 후 JWT를 생성하여 클라이언트에 반환한다.
클라이언트는 API 요청 시 Authorization: Bearer <JWT> 헤더를 포함하여 리소스 서버에 요청을 보낸다.
리소스 서버는 JWT의 서명을 검증하고, 토큰의 유효성을 확인한 후 요청을 처리한다.
OAuth2에서 JWT 기반 인증 흐름 상세 과정
1단계: 사용자 로그인 요청
사용자가 클라이언트 애플리케이션을 통해 로그인 요청을 보낸다. 일반적으로 로그인은 이메일과 비밀번호를 입력하거나, OAuth2를 이용한 소셜 로그인 방식(Google, Facebook 등)을 통해 진행된다.

2단계: 클라이언트가 OAuth2 인증 서버에 인증 요청
클라이언트 애플리케이션은 OAuth2 인증 서버에 인증 요청을 보낸다. 이때, 클라이언트는 client_id, client_secret 등의 정보를 함께 제공하여 서버가 요청을 검증할 수 있도록 한다.

Authorization Code Grant 방식의 예제:
POST /oauth/token HTTP/1.1
Host: auth.server.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&
code=AUTH_CODE_FROM_LOGIN&
redirect_uri=https://client.app/callback&
client_id=client123&
client_secret=secretKey
3단계: OAuth2 인증 서버에서 JWT 발급
OAuth2 인증 서버는 사용자의 인증 정보를 확인한 후, JWT를 생성하고 이를 액세스 토큰으로 반환한다.

JWT 응답 예제 (액세스 토큰)
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "Bearer",
  "expires_in": 3600,
  "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
여기서 access_token 값은 JWT이며, expires_in 값은 액세스 토큰의 유효 기간(초 단위)을 나타낸다.

4단계: 클라이언트가 리소스 서버에 API 요청 시 JWT 포함
클라이언트 애플리케이션은 API 요청을 보낼 때, 발급받은 JWT를 Authorization 헤더에 포함하여 전송한다.

GET /api/user/profile HTTP/1.1
Host: api.server.com
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
5단계: 리소스 서버에서 JWT 검증 및 요청 처리
리소스 서버(API 서버)는 클라이언트가 보낸 요청을 처리하기 전에, 포함된 JWT를 검증한다.

검증 과정은 다음과 같다.

JWT의 서명(Signature) 검증

서버는 JWT의 서명이 신뢰할 수 있는 인증 서버에서 생성된 것인지 확인한다.
서명이 올바르지 않다면 요청을 거부한다.
토큰 만료 여부 확인

exp(Expiration) 값을 확인하여 JWT가 만료되었는지 검사한다.
만료된 JWT는 사용할 수 없으며, 클라이언트는 새 토큰을 발급받아야 한다.
토큰의 클레임(Claim) 정보 확인

iss(Issuer): JWT의 발급자가 신뢰할 수 있는 인증 서버인지 확인한다.
aud(Audience): JWT가 현재 요청하는 API에 사용 가능한지 확인한다.
sub(Subject): 사용자 ID 정보를 가져온다.
scope(Scope): 사용자가 요청한 권한 범위를 확인한다.
6단계: 인증이 성공하면 리소스 서버가 요청을 처리
JWT가 유효하면, 서버는 사용자의 권한을 확인한 후 해당 API 요청을 정상적으로 처리한다.

JWT 검증 코드 예제 (Spring Security 적용)
Spring Boot 기반 리소스 서버에서 JWT 검증을 수행하는 예제 코드는 다음과 같다.

@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/api/user/profile").authenticated()
                .anyRequest().permitAll()
            )
            .oauth2ResourceServer(OAuth2ResourceServerConfigurer::jwt);
        return http.build();
    }

    @Bean
    public JwtDecoder jwtDecoder() {
        return NimbusJwtDecoder.withJwkSetUri("https://auth.server.com/.well-known/jwks.json").build();
    }
}
이 설정을 적용하면, Spring Security가 자동으로 JWT를 검증하고 요청을 인증하게 된다.

JWT 기반 OAuth2 인증의 이점
OAuth2에서 JWT를 사용하면 다음과 같은 장점이 있다.

인증 속도 향상

JWT는 자체 포함된(Self-contained) 토큰이므로, 별도의 DB 조회 없이 서명을 검증하여 인증을 수행할 수 있다.
API 서버는 매 요청마다 DB를 조회할 필요가 없어 성능이 향상된다.
확장성 높은 분산 시스템 구축 가능

JWT를 사용하면 중앙 인증 서버 없이 여러 개의 독립적인 리소스 서버에서 인증을 수행할 수 있다.
여러 마이크로서비스가 존재하는 환경에서 특히 유용하다.
안전한 권한 관리 가능

JWT의 Payload에 사용자의 역할(Role)과 권한(Scope)을 포함할 수 있으므로, API 접근을 보다 세밀하게 제어할 수 있다.
예를 들어, scope: "read write" 권한을 부여하면, 특정 API는 읽기만 가능하게 설정할 수 있다.
JWT 기반 OAuth2 인증의 한계점
토큰 취소(Revocation)가 어렵다

JWT는 자체 포함된 토큰이므로, 한 번 발급되면 서버에서 이를 취소할 방법이 없다.
따라서, 사용자가 로그아웃했거나 권한이 변경된 경우에도 기존 JWT는 여전히 유효할 수 있다.
해결책: 짧은 만료 시간(exp) 설정 + Refresh Token 사용.
Payload 데이터가 노출될 가능성

JWT의 Payload는 Base64 URL 인코딩되므로, 누구나 디코딩하여 내용을 확인할 수 있다.
따라서 비밀번호 같은 민감한 정보는 JWT에 저장하면 안 된다.
필요하면 JWE(JSON Web Encryption) 를 사용하여 암호화할 수 있다.
학습자의 사고를 돕기 위한 질문
OAuth2 기반 시스템에서 Access Token이 발급될 때, JWT를 사용하면 서버의 부하를 줄일 수 있는 이유는 무엇인가?

세션 기반 인증과 비교하여 서버의 부담이 어떻게 감소하는지 생각해보라.
JWT 기반의 OAuth2 인증이 적용될 경우, 사용자의 요청이 처리되는 과정에서 서버가 JWT를 검증하는 단계는 무엇인가?

클라이언트가 API 요청을 보낼 때 JWT가 어떻게 검증되는지 확인해보라.
실습 문제
문제 1: OAuth2 인증 서버에서 JWT 발급 흐름 이해
다음 요구사항을 만족하는 코드를 작성하시오.

OAuth2 인증 서버를 구성하여 JWT 기반의 Access Token을 발급한다.
클라이언트가 인증 요청을 보낼 때 필요한 정보를 명확하게 입력한다.
인증이 성공하면 발급된 JWT를 출력한다.
문제 2: JWT를 사용한 OAuth2 인증 검증 프로세스
다음 요구사항을 만족하는 코드를 작성하시오.

발급된 JWT를 사용하여 리소스 서버에 API 요청을 보낸다.
서버가 JWT를 검증하는 과정을 코드로 구현한다.
유효한 JWT의 경우 요청이 정상 처리되고, 유효하지 않은 JWT의 경우 인증 실패 메시지가 출력되도록 구현한다.
3.3. Access Token과 Refresh Token의 차이
OAuth2를 사용할 때, Access Token과 Refresh Token의 개념을 이해하는 것은 매우 중요하다. Access Token은 API 요청 시 사용자의 인증을 대신하는 토큰이고, Refresh Token은 만료된 Access Token을 재발급하는 역할을 한다.

이번 장에서는 Access Token과 Refresh Token의 차이점, 각각의 특징과 사용 방식, 그리고 보안상 고려해야 할 사항들을 다룬다.

Access Token과 Refresh Token의 개념
OAuth2 기반 인증 시스템에서 클라이언트가 API 요청을 할 때 직접적으로 사용되는 것은 Access Token이다. 하지만, Access Token은 보안상의 이유로 수명이 짧게 설정된다. 즉, 특정 시간이 지나면 자동으로 만료된다.

이와 반대로, Refresh Token은 보다 긴 수명을 가지며, Access Token이 만료되었을 때 새로운 Access Token을 발급받기 위해 사용된다.

Access Token과 Refresh Token의 주요 차이점은 다음과 같다.

토큰 유형	역할 및 특징
Access Token	API 요청 시 인증에 사용. 보안 강화를 위해 짧은 수명을 가짐.
Refresh Token	새로운 Access Token을 발급받을 때 사용. 긴 수명을 가지며, 클라이언트가 서버에 요청해 새 Access Token을 받을 수 있음.
Access Token의 동작 방식
Access Token은 클라이언트가 API를 호출할 때 사용되며, 보통 Authorization 헤더에 포함된다.
아래는 Access Token을 사용한 HTTP 요청 예제이다.

GET /api/user/profile HTTP/1.1
Host: api.server.com
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
리소스 서버(API 서버)는 이 토큰을 검증하고, 유효하면 사용자의 정보를 확인한 후 요청을 처리한다.
그러나 Access Token은 짧은 수명을 가지므로, 일정 시간이 지나면 만료되어 더 이상 사용할 수 없다.

Refresh Token의 동작 방식
Access Token이 만료되면, 클라이언트는 새로운 Access Token을 받기 위해 Refresh Token을 사용하여 OAuth2 인증 서버에 요청을 보낸다.
아래는 Refresh Token을 사용하여 새로운 Access Token을 요청하는 예제이다.

POST /oauth/token HTTP/1.1
Host: auth.server.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&
refresh_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...&
client_id=client123&
client_secret=secretKey
서버는 Refresh Token을 검증한 후 새로운 Access Token을 발급하여 클라이언트에 반환한다.

{
  "access_token": "new-access-token-value",
  "token_type": "Bearer",
  "expires_in": 3600
}
이제 클라이언트는 새로운 Access Token을 사용하여 API 요청을 계속 보낼 수 있다.

Access Token과 Refresh Token 사용 흐름
Access Token과 Refresh Token을 사용하는 OAuth2 인증 과정은 다음과 같이 진행된다.

클라이언트가 로그인하여 OAuth2 인증 서버에서 Access Token과 Refresh Token을 발급받는다.
클라이언트는 Access Token을 사용하여 리소스 서버에 API 요청을 보낸다.
Access Token이 만료되면, 클라이언트는 Refresh Token을 이용하여 새로운 Access Token을 요청한다.
OAuth2 인증 서버는 Refresh Token을 검증하고, 새로운 Access Token을 발급하여 반환한다.
클라이언트는 새로운 Access Token을 사용하여 다시 API 요청을 수행한다.
Access Token과 Refresh Token의 보안 고려 사항
Access Token과 Refresh Token을 안전하게 관리하기 위해서는 몇 가지 보안 조치가 필요하다.

Access Token의 수명을 짧게 설정해야 한다.

Access Token은 외부 API 요청 시 직접 사용되므로 탈취될 위험이 있다.
따라서 짧은 만료 시간을 설정하고, 만료된 후에는 Refresh Token을 통해 새로 발급받도록 해야 한다.
Refresh Token은 서버에서 안전하게 저장해야 한다.

Refresh Token은 Access Token보다 더 긴 수명을 가지므로, 이를 안전하게 관리해야 한다.
Refresh Token이 탈취되면 새로운 Access Token을 계속 발급받을 수 있기 때문에, 보안이 중요하다.
Refresh Token을 클라이언트에 저장하는 방식 고려

웹 애플리케이션에서는 Refresh Token을 HttpOnly 쿠키에 저장하는 것이 일반적이다.
모바일 애플리케이션에서는 보안 저장소(예: iOS Keychain, Android EncryptedSharedPreferences)에 저장할 수 있다.
Refresh Token의 사용 제한

Refresh Token을 한 번 사용하면 새로운 Refresh Token을 발급하고 기존의 Refresh Token은 폐기해야 한다.
이를 통해 탈취된 Refresh Token을 재사용하는 것을 방지할 수 있다.
Refresh Token을 주기적으로 갱신

Refresh Token도 만료 기간을 설정해야 한다.
일정 기간이 지나면 사용자가 다시 로그인하도록 요구하여 보안을 강화할 수 있다.
Spring Security에서 Access Token과 Refresh Token 관리
Spring Security 기반의 OAuth2 인증 서버에서 Access Token과 Refresh Token을 발급하고 검증하는 예제 코드는 다음과 같다.

@Configuration
@EnableAuthorizationServer
public class AuthorizationServerConfig extends AuthorizationServerConfigurerAdapter {

    @Override
    public void configure(ClientDetailsServiceConfigurer clients) throws Exception {
        clients.inMemory()
            .withClient("client123")
            .secret("{noop}secretKey")
            .authorizedGrantTypes("password", "refresh_token")
            .scopes("read", "write")
            .accessTokenValiditySeconds(3600) // Access Token 유효 시간: 1시간
            .refreshTokenValiditySeconds(86400); // Refresh Token 유효 시간: 1일
    }
}
이 설정을 적용하면, Access Token과 Refresh Token을 각각 1시간, 24시간 동안 유효하도록 관리할 수 있다.

Access Token과 Refresh Token을 사용하는 이유
Access Token과 Refresh Token을 사용하는 이유는 보안성과 성능을 모두 고려한 설계 때문이다.

Access Token을 짧게 설정함으로써 보안을 강화한다.

해킹당하더라도 금방 만료되기 때문에 피해를 줄일 수 있다.
Refresh Token을 통해 사용자가 다시 로그인하지 않고도 Access Token을 갱신할 수 있다.

사용자가 매번 로그인할 필요 없이 백그라운드에서 자동으로 인증을 갱신할 수 있다.
리소스 서버(API 서버)의 부담을 줄일 수 있다.

Access Token 검증은 빠르게 진행할 수 있으며, DB 조회 없이 검증할 수 있도록 설계 가능하다.
학습자의 사고를 돕기 위한 질문
Access Token과 Refresh Token은 각각 언제 사용되며, Refresh Token이 필요한 이유는 무엇인가?

보안성과 토큰 재발급의 효율성을 고려해보라.
Refresh Token이 Access Token보다 보안 측면에서 더 강력하게 보호되어야 하는 이유는 무엇인가?

Refresh Token이 탈취되었을 때 발생할 수 있는 문제를 생각해보라.
4. Spring Security에서 OAuth2 및 JWT 통합
4.1. OAuth2 인증 구현
OAuth2 인증을 Spring Security에서 구현하려면 OAuth2 Client, Authorization Server, Resource Server를 설정해야 한다.
이 장에서는 OAuth2 인증의 기본 개념을 설명하고, Spring Security를 활용하여 OAuth2 인증을 구현하는 방법을 다룬다.

OAuth2 인증 흐름
OAuth2 인증의 주요 흐름은 다음과 같다.

클라이언트(Client) : 사용자의 인증을 위해 OAuth2 인증 서버에 요청을 보낸다.
Authorization Server(인증 서버) : 사용자 인증 후 Access Token을 발급한다.
Resource Server(리소스 서버) : 클라이언트가 Access Token을 사용하여 보호된 API에 접근할 수 있도록 한다.
사용자(User) : OAuth2 인증 서버를 통해 인증을 진행한다.
Spring Security를 활용한 OAuth2 인증 구성
OAuth2 인증을 Spring Security에서 구현하려면 spring-security-oauth2-client 및 spring-security-oauth2-resource-server 라이브러리를 활용한다.

우선, build.gradle에 필요한 라이브러리를 추가한다.

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-oauth2-client'
    implementation 'org.springframework.boot:spring-boot-starter-oauth2-resource-server'
}
OAuth2 Client 설정
OAuth2 클라이언트를 설정하기 위해 application.yml 파일에서 OAuth2 Provider(Google, Facebook, Naver, Kakao 등)를 설정할 수 있다.

spring:
  security:
    oauth2:
      client:
        registration:
          google:
            client-id: your-client-id
            client-secret: your-client-secret
            scope: profile, email
          github:
            client-id: your-github-client-id
            client-secret: your-github-client-secret
            scope: user:email
client-id : OAuth2 인증을 위해 등록된 클라이언트 ID
client-secret : OAuth2 클라이언트의 비밀 키
scope : OAuth2에서 요청할 사용자 정보 범위
OAuth2 Client는 사용자가 로그인하면 OAuth2 Provider(Google, GitHub 등) 에서 사용자 정보를 받아올 수 있도록 한다.

OAuth2 Client를 활용한 로그인 구현
Spring Security를 활용하여 OAuth2 로그인을 적용하려면 SecurityFilterChain을 설정해야 한다.

@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/", "/login").permitAll()
                .anyRequest().authenticated()
            )
            .oauth2Login(); // OAuth2 로그인 활성화

        return http.build();
    }
}
위 설정을 통해 OAuth2 로그인을 활성화할 수 있으며, 사용자는 /oauth2/authorization/{provider} 엔드포인트를 통해 로그인할 수 있다.

예를 들어, Google OAuth2 로그인을 수행하려면 다음과 같은 URL을 호출하면 된다.

https://your-app.com/oauth2/authorization/google
OAuth2 Provider(Google 등)에서 인증이 완료되면, Spring Security는 자동으로 사용자 정보를 가져와 세션에 저장한다.

OAuth2 Authorization Server 설정
OAuth2 Authorization Server는 Access Token 및 Refresh Token을 발급하는 역할을 수행한다.
Spring Security를 사용하여 Authorization Server를 설정하려면 spring-authorization-server 라이브러리를 추가해야 한다.

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-oauth2-authorization-server'
}
Authorization Server를 설정하기 위해 SecurityConfig에 @EnableAuthorizationServer를 추가하고, Access Token을 발급하는 엔드포인트를 정의한다.

@Configuration
@EnableAuthorizationServer
public class AuthorizationServerConfig extends AuthorizationServerConfigurerAdapter {

    @Override
    public void configure(ClientDetailsServiceConfigurer clients) throws Exception {
        clients.inMemory()
            .withClient("client-id")
            .secret("{noop}client-secret")
            .authorizedGrantTypes("authorization_code", "refresh_token", "password")
            .scopes("read", "write")
            .accessTokenValiditySeconds(3600) // Access Token 유효 시간: 1시간
            .refreshTokenValiditySeconds(86400); // Refresh Token 유효 시간: 1일
    }
}
이 설정을 통해 클라이언트는 Access Token과 Refresh Token을 받을 수 있으며, OAuth2 인증 서버가 토큰을 관리하도록 설정할 수 있다.

OAuth2 Resource Server 설정
OAuth2 인증 후 발급된 Access Token을 검증하고 API 접근을 제어하는 역할을 수행하는 것이 Resource Server이다.
Spring Security에서 Resource Server를 설정하려면 spring-security-oauth2-resource-server 라이브러리를 사용해야 한다.

spring:
  security:
    oauth2:
      resourceserver:
        jwt:
          issuer-uri: https://auth.server.com
Resource Server 설정을 추가하면 OAuth2 Access Token을 검증하고 보호된 API에 접근할 수 있다.
다음과 같이 Spring Security 설정에서 Resource Server를 활성화할 수 있다.

@Configuration
@EnableWebSecurity
public class ResourceServerConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/public").permitAll()
                .requestMatchers("/api/**").authenticated()
            )
            .oauth2ResourceServer(OAuth2ResourceServerConfigurer::jwt);

        return http.build();
    }
}
이 설정을 적용하면 JWT를 검증하여 API 요청을 처리할 수 있다.

OAuth2 인증을 위한 application.yml 구성
OAuth2 인증 설정을 application.yml에서 구성할 수 있다.
아래는 OAuth2 Authorization Server와 Resource Server를 설정하는 예제이다.

spring:
  security:
    oauth2:
      authorizationserver:
        client:
          client-id:
            registration:
              provider: custom
              client-id: your-client-id
              client-secret: your-client-secret
              scope: openid, profile, email
              authorization-grant-type: authorization_code
              redirect-uri: "{baseUrl}/login/oauth2/code/{registrationId}"
      resourceserver:
        jwt:
          issuer-uri: https://auth.server.com
OAuth2 인증 방식별 적용
Spring Security에서 OAuth2 인증 방식은 크게 세 가지로 나뉜다.

OAuth2 Login

사용자가 소셜 로그인(Google, Facebook 등)을 사용하여 인증하는 방식
oauth2Login()을 통해 활성화
OAuth2 Authorization Server

클라이언트가 자체적으로 OAuth2 인증을 처리할 수 있도록 Authorization Server 설정
@EnableAuthorizationServer 설정을 추가
OAuth2 Resource Server

JWT 기반 인증을 사용하여 API 접근을 제어하는 방식
oauth2ResourceServer(OAuth2ResourceServerConfigurer::jwt)를 사용하여 Access Token 검증
이처럼 OAuth2 인증을 적용하는 방식은 각 애플리케이션의 요구 사항에 따라 다를 수 있다.

실습 문제
문제 1: OAuth2 인증 서버 설정
아래 요구사항을 만족하는 코드를 작성하시오.

Spring Boot와 Spring Security를 사용하여 OAuth2 인증 서버를 설정한다.
클라이언트가 OAuth2 인증 요청을 보내고, 인증이 성공하면 Access Token을 반환한다.
인증 요청 시 클라이언트 ID와 클라이언트 비밀번호를 요구하도록 구성한다.
문제 2: OAuth2 클라이언트 설정
다음 요구사항을 만족하는 코드를 작성하시오.

OAuth2 클라이언트를 설정하여 인증 서버에 요청을 보낸다.
인증이 완료되면 발급된 Access Token을 저장하고 출력한다.
OAuth2 인증 방식 중 Authorization Code Grant를 사용한다.
4.2. Spring Security에서 JWT 적용
Spring Security에서 JWT(JSON Web Token) 를 활용한 인증을 적용하는 과정은 크게 토큰 발급, 검증, 및 인증 필터 설정으로 나뉜다.
이 장에서는 Spring Security에서 JWT를 활용하는 방법을 자세히 설명한다.

JWT 인증 방식 개요
JWT를 활용한 인증의 핵심 개념은 다음과 같다.

사용자가 로그인 요청을 보냄
서버에서 사용자를 인증한 후 JWT를 발급
클라이언트가 JWT를 포함하여 API 요청을 보냄
서버에서 JWT를 검증하여 사용자 인증을 수행
JWT 기반 인증의 가장 큰 특징은 서버가 세션을 유지할 필요가 없다는 점이다.
즉, Stateless(무상태) 방식으로 동작하며, 사용자의 인증 상태를 클라이언트에서 유지할 수 있다.

Spring Security에서 JWT 발급 및 검증 설정
JWT를 Spring Security에서 사용하려면 Security Filter Chain을 활용하여 인증 필터를 적용해야 한다.
먼저, JWT를 발급하고 검증할 수 있도록 JwtDecoder와 JwtEncoder를 설정해야 한다.

@Configuration
@EnableWebSecurity
public class SecurityConfig {

    private final JwtDecoder jwtDecoder;
    private final JwtEncoder jwtEncoder;

    public SecurityConfig(JwtDecoder jwtDecoder, JwtEncoder jwtEncoder) {
        this.jwtDecoder = jwtDecoder;
        this.jwtEncoder = jwtEncoder;
    }

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/public/**").permitAll()  // 인증이 필요 없는 API
                .requestMatchers("/api/**").authenticated() // 인증이 필요한 API
            )
            .oauth2ResourceServer(oauth2 -> oauth2
                .jwt(jwt -> jwt.decoder(jwtDecoder)) // JWT 인증 적용
            );

        return http.build();
    }
}
jwtDecoder : 클라이언트가 보낸 JWT를 해석하여 검증
jwtEncoder : JWT를 발급하는 역할
위 설정을 적용하면 JWT를 기반으로 한 API 인증을 수행할 수 있다.

JWT 발급을 위한 Security 설정
Spring Security에서 JWT를 발급하려면 사용자 인증 후 JWT를 생성하는 로직이 필요하다.
아래는 JWT를 생성하는 JwtTokenProvider 클래스의 예제이다.

@Component
public class JwtTokenProvider {

    private final JwtEncoder jwtEncoder;

    public JwtTokenProvider(JwtEncoder jwtEncoder) {
        this.jwtEncoder = jwtEncoder;
    }

    public String generateToken(Authentication authentication) {
        Instant now = Instant.now();
        long expiry = 3600; // 1시간 후 만료

        JwtClaimsSet claims = JwtClaimsSet.builder()
                .subject(authentication.getName()) // 사용자 이름 설정
                .issuedAt(now)
                .expiresAt(now.plusSeconds(expiry))
                .claim("roles", authentication.getAuthorities().stream()
                        .map(GrantedAuthority::getAuthority)
                        .collect(Collectors.toList()))
                .build();

        return this.jwtEncoder.encode(JwtEncoderParameters.from(claims)).getTokenValue();
    }
}
JwtEncoder : JWT를 생성하는 역할
JwtClaimsSet : JWT 내부의 Payload를 정의하는 객체
expiresAt : 토큰의 만료 시간을 설정
이제 사용자가 로그인하면 JWT를 발급하여 반환할 수 있다.

JWT 검증을 위한 Security 설정
클라이언트가 API 요청 시, Authorization 헤더에 JWT를 포함하여 요청을 보내면, 서버에서는 이를 검증해야 한다.
Spring Security에서 JWT 검증을 수행하는 JwtDecoder를 설정할 수 있다.

@Bean
public JwtDecoder jwtDecoder() {
    return NimbusJwtDecoder.withSecretKey(secretKey()).build();
}

@Bean
public Key secretKey() {
    return new SecretKeySpec("your-secret-key".getBytes(), "HmacSHA256");
}
jwtDecoder : JWT의 서명을 검증하고 Payload를 파싱
secretKey : 대칭 키 기반의 서명을 위한 키 설정
이제 클라이언트가 유효한 JWT를 포함하여 API를 호출하면, 서버는 이를 검증한 후 인증을 수행한다.

JWT 인증 필터 적용
JWT를 활용한 인증을 수행하려면 Spring Security 필터를 추가해야 한다.
아래 JwtAuthenticationFilter는 요청을 가로채 JWT를 검증하는 역할을 수행한다.

@Component
public class JwtAuthenticationFilter extends OncePerRequestFilter {

    private final JwtDecoder jwtDecoder;
    private final AuthenticationManager authenticationManager;

    public JwtAuthenticationFilter(JwtDecoder jwtDecoder, AuthenticationManager authenticationManager) {
        this.jwtDecoder = jwtDecoder;
        this.authenticationManager = authenticationManager;
    }

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain chain)
            throws ServletException, IOException {
        String token = resolveToken(request);

        if (token != null) {
            try {
                Jwt jwt = jwtDecoder.decode(token);
                Authentication authentication = getAuthentication(jwt);
                SecurityContextHolder.getContext().setAuthentication(authentication);
            } catch (JwtException e) {
                response.sendError(HttpServletResponse.SC_UNAUTHORIZED, "Invalid JWT token");
                return;
            }
        }

        chain.doFilter(request, response);
    }

    private String resolveToken(HttpServletRequest request) {
        String bearerToken = request.getHeader("Authorization");
        if (StringUtils.hasText(bearerToken) && bearerToken.startsWith("Bearer ")) {
            return bearerToken.substring(7);
        }
        return null;
    }

    private Authentication getAuthentication(Jwt jwt) {
        List<GrantedAuthority> authorities = jwt.getClaim("roles").stream()
                .map(role -> new SimpleGrantedAuthority((String) role))
                .collect(Collectors.toList());

        return new UsernamePasswordAuthenticationToken(jwt.getSubject(), null, authorities);
    }
}
doFilterInternal() : 요청을 가로채 JWT를 검증
resolveToken() : HTTP 요청에서 Authorization 헤더를 파싱하여 토큰을 추출
getAuthentication() : JWT의 Claims에서 사용자 정보를 가져와 Authentication 객체로 변환
이제 Spring Security에서 JWT 기반 인증을 필터로 처리할 수 있다.

JWT 설정을 위한 application.yml 구성
JWT의 발급 및 검증을 위해 application.yml 파일에서 Secret Key 및 설정을 정의할 수 있다.

spring:
  security:
    oauth2:
      resourceserver:
        jwt:
          issuer-uri: https://your-auth-server.com
          jwk-set-uri: https://your-auth-server.com/oauth2/jwks
issuer-uri : JWT를 발급한 서버의 주소
jwk-set-uri : JSON Web Key Set(JWKS) URL (비대칭 키 기반 JWT 사용 시 필요)
JWT 인증 적용 방식
Spring Security에서 JWT를 적용하는 방법은 크게 세 가지로 나뉜다.

JWT를 통한 OAuth2 Resource Server 인증

JwtDecoder를 사용하여 Access Token을 검증
oauth2ResourceServer(OAuth2ResourceServerConfigurer::jwt) 설정 적용
JWT를 활용한 사용자 인증 및 권한 부여

JWT 내부의 claims를 활용하여 사용자 역할(Role) 부여
Spring Security의 @PreAuthorize 및 @PostAuthorize를 적용하여 접근 제어
JWT Refresh Token을 활용한 인증 갱신

Access Token이 만료되면 Refresh Token을 활용하여 새로운 JWT를 발급
Refresh Token을 저장하고 보안성을 고려한 처리 방식 적용
이와 같이 JWT를 활용하면 Spring Security에서 세션 없이도 안전한 인증을 구현할 수 있다.

실습 문제
문제 1: JWT를 사용한 인증 필터 구현
아래 요구사항을 만족하는 코드를 작성하시오.

Spring Security의 필터를 확장하여 JWT 인증 필터를 구현한다.
HTTP 요청의 Authorization 헤더에서 JWT를 추출하고 검증한다.
유효한 토큰일 경우 SecurityContext에 사용자 정보를 저장한다.
문제 2: JWT 기반 로그인 구현
다음 요구사항을 만족하는 코드를 작성하시오.

사용자가 로그인 시 JWT를 생성하여 반환하는 API를 구현한다.
JWT는 사용자 ID와 역할(Role) 정보를 포함하도록 설정한다.
인증이 완료되면 발급된 JWT를 클라이언트에 반환한다.
4.3. OAuth2 및 JWT 설정을 위한 주요 컴포넌트
OAuth2와 JWT 기반 인증을 구현할 때는 Spring Security의 여러 주요 컴포넌트를 활용하게 된다.
이 장에서는 OAuth2 및 JWT 설정을 위해 필수적으로 알아야 할 주요 컴포넌트를 상세히 설명한다.

AuthenticationManager의 역할
AuthenticationManager는 Spring Security에서 사용자의 인증(Authentication)을 처리하는 핵심 인터페이스이다.
사용자가 로그인을 시도할 때, AuthenticationManager는 입력된 자격 증명을 검증하고 적절한 인증 객체(Authentication)를 반환한다.

@Bean
public AuthenticationManager authenticationManager(AuthenticationConfiguration authenticationConfiguration)
        throws Exception {
    return authenticationConfiguration.getAuthenticationManager();
}
AuthenticationManager는 사용자의 인증 요청을 검증하는 역할을 수행한다.
내부적으로 AuthenticationProvider를 호출하여 사용자 인증 절차를 위임한다.
인증이 성공하면, 인증된 사용자 정보(Authentication)를 반환하고, 실패하면 예외를 발생시킨다.
SecurityContextHolder를 활용한 인증 정보 저장
Spring Security에서 인증된 사용자 정보를 저장하고 관리하는 객체가 SecurityContextHolder이다.
SecurityContextHolder는 현재 요청의 인증 상태를 유지하며, 이를 통해 애플리케이션 전반에서 인증 정보를 활용할 수 있다.

Authentication authentication = SecurityContextHolder.getContext().getAuthentication();
위 코드를 실행하면 현재 로그인한 사용자의 인증 정보를 가져올 수 있다.

SecurityContextHolder의 동작 방식
사용자가 로그인 요청을 보냄
AuthenticationManager가 사용자를 인증하고 Authentication 객체를 생성
인증이 완료되면 SecurityContextHolder에 Authentication 객체를 저장
이후의 모든 요청에서 SecurityContextHolder를 통해 사용자 정보를 조회 가능
JwtDecoder와 JwtEncoder를 활용한 JWT 처리
Spring Security에서 JWT를 활용하려면 JwtDecoder와 JwtEncoder를 사용해야 한다.

JwtDecoder: JWT 검증을 담당
JWT가 요청의 Authorization 헤더에 포함되어 있을 경우, 서버는 이를 검증해야 한다.
이를 수행하는 컴포넌트가 JwtDecoder이다.

@Bean
public JwtDecoder jwtDecoder() {
    return NimbusJwtDecoder.withSecretKey(secretKey()).build();
}

@Bean
public Key secretKey() {
    return new SecretKeySpec("your-secret-key".getBytes(), "HmacSHA256");
}
jwtDecoder()는 Authorization 헤더에서 JWT를 가져와 디코딩 및 검증한다.
NimbusJwtDecoder.withSecretKey()를 사용하여 대칭키(HMAC) 기반의 JWT 검증을 수행한다.
비대칭키(RSA, ECDSA)를 사용할 경우 NimbusJwtDecoder.withPublicKey()를 사용할 수 있다.
JwtEncoder: JWT 생성 및 서명
JwtEncoder는 새로운 JWT를 발급할 때 사용된다.

@Bean
public JwtEncoder jwtEncoder() {
    return new NimbusJwtEncoder(new ImmutableSecret<>(secretKey().getEncoded()));
}
JwtEncoder는 서버에서 사용자가 로그인할 때 JWT를 생성하는 역할을 한다.
ImmutableSecret<>(secretKey().getEncoded())를 통해 HMAC 기반 서명을 적용한다.
JWT의 Payload를 설정하여 사용자 정보와 만료 시간 등을 포함할 수 있다.
JwtAuthenticationConverter를 이용한 권한 변환
JWT에는 사용자의 역할(Role) 및 권한(Authorities)이 포함될 수 있다.
이를 JwtAuthenticationConverter를 활용하여 Spring Security의 GrantedAuthority 객체로 변환할 수 있다.

@Component
public class JwtAuthenticationConverter implements Converter<Jwt, AbstractAuthenticationToken> {

    @Override
    public AbstractAuthenticationToken convert(Jwt jwt) {
        Collection<GrantedAuthority> authorities = jwt.getClaim("roles").stream()
                .map(role -> new SimpleGrantedAuthority("ROLE_" + role))
                .collect(Collectors.toList());

        return new UsernamePasswordAuthenticationToken(jwt.getSubject(), jwt, authorities);
    }
}
JwtAuthenticationConverter는 JWT 내부의 "roles" 클레임을 GrantedAuthority로 변환한다.
ROLE_ 접두사를 붙여 Spring Security에서 권한을 인식할 수 있도록 설정한다.
변환된 권한 정보는 Spring Security의 인증 객체에 저장되며, @PreAuthorize 등의 접근 제어에서 활용할 수 있다.
SecurityFilterChain에서 JWT 인증 적용
이제 위의 설정들을 Spring Security 필터 체인에 적용하여 JWT 인증을 활성화해야 한다.

@Configuration
@EnableWebSecurity
public class SecurityConfig {

    private final JwtDecoder jwtDecoder;
    private final JwtEncoder jwtEncoder;
    private final JwtAuthenticationConverter jwtAuthenticationConverter;

    public SecurityConfig(JwtDecoder jwtDecoder, JwtEncoder jwtEncoder,
                          JwtAuthenticationConverter jwtAuthenticationConverter) {
        this.jwtDecoder = jwtDecoder;
        this.jwtEncoder = jwtEncoder;
        this.jwtAuthenticationConverter = jwtAuthenticationConverter;
    }

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/public/**").permitAll()
                .requestMatchers("/api/**").authenticated()
            )
            .oauth2ResourceServer(oauth2 -> oauth2
                .jwt(jwt -> jwt
                    .decoder(jwtDecoder)
                    .jwtAuthenticationConverter(jwtAuthenticationConverter)
                )
            );

        return http.build();
    }
}
jwtDecoder를 적용하여 JWT를 이용한 인증을 수행한다.
jwtAuthenticationConverter를 설정하여 JWT 내부의 역할(Role)을 GrantedAuthority로 변환한다.
oauth2ResourceServer().jwt()를 활용하여 JWT를 인증 방식으로 사용하는 API 서버를 구성한다.
@PreAuthorize 및 @PostAuthorize를 활용한 권한 제어
Spring Security에서는 @PreAuthorize 및 @PostAuthorize를 활용하여 메소드 실행 전후로 권한을 검사할 수 있다.
JWT를 활용한 인증이 적용되었다면, 다음과 같이 특정 역할(Role)이 있는 사용자만 접근할 수 있도록 설정할 수 있다.

@RestController
@RequestMapping("/admin")
public class AdminController {

    @GetMapping("/dashboard")
    @PreAuthorize("hasRole('ADMIN')")
    public String adminDashboard() {
        return "Admin Dashboard";
    }
}
@PreAuthorize("hasRole('ADMIN')"): "ROLE_ADMIN" 권한이 있는 사용자만 접근 가능
@PostAuthorize("returnObject.owner == authentication.name"): 메소드 실행 후, 반환된 객체의 소유자가 현재 사용자와 일치하는지 확인 가능
Refresh Token을 활용한 JWT 인증 갱신
JWT 기반 인증을 사용할 때, Access Token이 만료되었을 때 새롭게 발급하는 방법이 필요하다.
이를 위해 Refresh Token을 활용하여 JWT를 갱신하는 API를 구성할 수 있다.

@RestController
@RequestMapping("/auth")
public class AuthController {

    private final JwtTokenProvider jwtTokenProvider;

    public AuthController(JwtTokenProvider jwtTokenProvider) {
        this.jwtTokenProvider = jwtTokenProvider;
    }

    @PostMapping("/refresh")
    public ResponseEntity<?> refreshToken(@RequestHeader("Authorization") String refreshToken) {
        String newAccessToken = jwtTokenProvider.refreshAccessToken(refreshToken);
        return ResponseEntity.ok(Map.of("accessToken", newAccessToken));
    }
}
사용자가 Refresh Token을 전송하면, 새로운 Access Token을 발급하여 반환한다.
Refresh Token은 일반적으로 데이터베이스 또는 Redis에 저장하여 검증 과정을 거친다.
Refresh Token이 유효하지 않으면 401 Unauthorized 응답을 반환한다.
실습 문제
문제 1: JwtDecoder와 JwtEncoder를 사용한 JWT 발급 및 검증
아래 요구사항을 만족하는 코드를 작성하시오.

Spring Security에서 제공하는 JwtDecoder와 JwtEncoder를 활용하여 JWT를 발급한다.
발급된 JWT를 검증하는 API를 구현한다.
유효한 JWT일 경우 사용자 정보를 반환하고, 유효하지 않은 경우 예외를 발생시킨다.
문제 2: AuthenticationManager와 SecurityContextHolder를 활용한 사용자 인증
다음 요구사항을 만족하는 코드를 작성하시오.

AuthenticationManager를 사용하여 사용자를 인증하고 JWT를 발급한다.
SecurityContextHolder를 사용하여 현재 인증된 사용자의 정보를 가져오는 API를 구현한다.
JWT를 포함한 요청이 들어올 경우, SecurityContext에서 사용자 정보를 읽어 처리한다.
5. JWT 발급 및 검증 구현
5.1. JWT 생성 및 서명
JWT(Json Web Token)는 사용자의 인증 정보를 포함한 토큰을 생성하여 클라이언트와 서버 간에 효율적인 인증을 수행할 수 있도록 한다.
이 과정에서 JWT의 보안성을 보장하기 위해 서명(Signature) 과정이 필수적이다.

JWT 생성 및 서명 과정은 크게 다음과 같은 절차를 따른다.

Header 생성: 알고리즘 및 토큰 타입 지정
Payload 생성: 사용자 정보 및 토큰 만료 시간 포함
Signature 생성: 비밀키를 사용하여 서명
이제 각 과정을 구체적으로 살펴보자.

JWT Header 생성
JWT의 Header(헤더) 는 토큰의 형식과 서명 알고리즘을 지정하는 역할을 한다.
헤더는 Base64 URL 인코딩된 JSON 형식으로 표현되며, 일반적으로 다음과 같은 구조를 가진다.

{
  "alg": "HS256",
  "typ": "JWT"
}
"alg": 서명에 사용할 알고리즘(예: HS256 → HMAC SHA-256)
"typ": 토큰 유형(일반적으로 "JWT" 사용)
서버에서는 Spring Security의 JwtEncoder 를 사용하여 이 정보를 자동으로 설정할 수 있다.

JWT Payload 생성
JWT의 Payload(페이로드) 는 토큰에 포함될 사용자 정보 및 추가 데이터를 포함한다.
이 역시 JSON 형식으로 작성되며, 주요 클레임(Claim)들은 다음과 같다.

{
  "sub": "user123",
  "iat": 1710150000,
  "exp": 1710153600,
  "roles": ["USER"]
}
"sub": Subject(사용자 ID 또는 식별 정보)
"iat": Issued At(토큰이 생성된 시간, UNIX Timestamp)
"exp": Expiration Time(토큰 만료 시간, UNIX Timestamp)
"roles": 사용자 역할(예: USER, ADMIN)
이 정보들은 Base64 URL 인코딩되어 JWT의 Payload 부분을 구성하게 된다.

JWT Signature 생성
JWT의 Signature(서명) 는 토큰이 변조되지 않았음을 보장하는 역할을 한다.
서명은 다음과 같은 방식으로 생성된다.

HMACSHA256(
  base64UrlEncode(header) + "." + base64UrlEncode(payload),
  secretKey
)
HMACSHA256: 서명 알고리즘(예: HMAC SHA-256)
base64UrlEncode(header): JWT의 헤더를 Base64 URL 인코딩
base64UrlEncode(payload): JWT의 페이로드를 Base64 URL 인코딩
secretKey: 서버에서 사용하는 서명용 비밀키
서버에서는 JwtEncoder를 활용하여 자동으로 서명을 적용할 수 있다.

Spring Security에서 JWT 생성
이제 JwtEncoder를 활용하여 JWT를 생성하는 코드를 작성해 보자.

@Component
public class JwtTokenProvider {

    private final JwtEncoder jwtEncoder;

    public JwtTokenProvider(JwtEncoder jwtEncoder) {
        this.jwtEncoder = jwtEncoder;
    }

    public String generateToken(String username, List<String> roles) {
        Instant now = Instant.now();
        long expiry = 3600L; // 1시간 유효

        JwtClaimsSet claims = JwtClaimsSet.builder()
                .subject(username)
                .issuedAt(now)
                .expiresAt(now.plusSeconds(expiry))
                .claim("roles", roles)
                .build();

        return this.jwtEncoder.encode(JwtEncoderParameters.from(claims)).getTokenValue();
    }
}
설명

JwtEncoder를 활용하여 JWT를 생성한다.
JwtClaimsSet.builder()를 사용하여 Payload에 사용자 정보 및 만료 시간 포함.
encode()를 통해 서명이 적용된 JWT를 최종 생성.
Spring Security에서 JWT 서명 알고리즘 설정
JWT의 보안성을 강화하기 위해 HMAC SHA-256 또는 RSA 서명 방식을 사용할 수 있다.
서명 알고리즘을 설정하는 방법은 다음과 같다.

HMAC (대칭 키) 기반 서명

@Bean
public JwtEncoder jwtEncoder() {
    return new NimbusJwtEncoder(new ImmutableSecret<>(secretKey().getEncoded()));
}

@Bean
public Key secretKey() {
    return new SecretKeySpec("your-secret-key".getBytes(), "HmacSHA256");
}
secretKey()에서 HMAC SHA-256 비밀키를 설정.
jwtEncoder()는 HMAC 기반 서명을 사용하도록 구성.
RSA (비대칭 키) 기반 서명

@Bean
public JwtEncoder jwtEncoder() {
    return new NimbusJwtEncoder(new ImmutableSecret<>(privateKey().getEncoded()));
}

@Bean
public Key privateKey() {
    return KeyFactory.getInstance("RSA").generatePrivate(new PKCS8EncodedKeySpec(privateKeyBytes));
}
privateKey()에서 RSA 개인 키를 설정.
RSA 방식은 공개키/개인키 기반의 서명 방식을 사용하여 더 높은 보안성을 제공.
JWT를 활용한 사용자 로그인 및 토큰 발급 API
JWT를 활용하면 사용자가 로그인할 때 Access Token을 발급할 수 있다.
다음은 JWT 기반 로그인 API의 예제 코드이다.

@RestController
@RequestMapping("/auth")
public class AuthController {

    private final AuthenticationManager authenticationManager;
    private final JwtTokenProvider jwtTokenProvider;

    public AuthController(AuthenticationManager authenticationManager, JwtTokenProvider jwtTokenProvider) {
        this.authenticationManager = authenticationManager;
        this.jwtTokenProvider = jwtTokenProvider;
    }

    @PostMapping("/login")
    public ResponseEntity<?> login(@RequestBody LoginRequest request) {
        Authentication authentication = authenticationManager.authenticate(
                new UsernamePasswordAuthenticationToken(request.getUsername(), request.getPassword()));

        String token = jwtTokenProvider.generateToken(request.getUsername(), List.of("USER"));

        return ResponseEntity.ok(Map.of("accessToken", token));
    }
}
설명

사용자가 로그인하면 AuthenticationManager를 통해 인증을 수행한다.
인증이 성공하면 JwtTokenProvider를 사용하여 JWT Access Token을 생성한다.
클라이언트에게 Access Token을 응답으로 반환.
JWT 발급 후 Access Token 사용 방식
JWT를 발급받은 클라이언트는 이후의 API 요청에서 Authorization 헤더를 사용하여 토큰을 전송한다.

Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR...
서버는 이 토큰을 검증하여 사용자의 인증 상태를 확인할 수 있다.
JWT의 검증 및 인증 처리 과정은 다음 장에서 다룬다.

실습 문제
문제 1: HMAC 기반의 JWT 생성
아래 요구사항을 만족하는 코드를 작성하시오.

jsonwebtoken 라이브러리를 사용하여 HMAC 알고리즘으로 JWT를 생성한다.
JWT는 사용자 ID, 역할(Role) , 토큰 만료 시간을 포함해야 한다.
생성된 JWT를 출력한다.
문제 2: RSA 기반의 JWT 서명
다음 요구사항을 만족하는 코드를 작성하시오.

RSA 키 쌍(공개 키 및 개인 키)을 생성하여 JWT를 서명한다.
클라이언트에서 JWT를 전송하면 공개 키를 사용하여 검증한다.
유효한 경우 사용자 정보를 반환하고, 유효하지 않은 경우 예외를 발생시킨다.
5.2. JWT 검증 및 인증 처리
JWT(Json Web Token)는 사용자 인증을 위한 강력한 방식이지만, 보안성을 유지하기 위해 반드시 토큰 검증 과정이 필요하다.
이 절에서는 JWT의 검증 방식과 Spring Security를 활용한 JWT 인증 처리에 대해 자세히 다룬다.

JWT 검증의 필요성
JWT는 사용자 정보를 포함한 디지털 서명된 토큰이다.
그러나 클라이언트가 서버로부터 받은 JWT를 임의로 변경하거나 위조할 가능성이 존재한다.
따라서 서버는 다음 사항을 검증해야 한다.

토큰 구조가 올바른지 확인
서명이 유효한지 확인
토큰의 만료 시간을 검증
Payload(페이로드) 데이터가 변조되지 않았는지 확인
권한(Role) 정보가 적절한지 확인
이제 각 검증 단계를 자세히 살펴보자.

JWT 검증 방식
JWT 검증은 다음의 절차로 진행된다.

토큰 형식 확인

클라이언트가 보낸 Authorization 헤더에 Bearer 토큰이 있는지 확인.
서명(Signature) 검증

HMAC 또는 RSA 등의 서명 알고리즘을 사용하여 토큰 변조 여부 확인.
토큰 만료 시간(Expiration) 확인

exp 클레임(Claim) 값을 비교하여 만료된 토큰인지 판별.
Payload 데이터 검증

사용자 ID, 역할(Role) 정보가 올바른지 확인.
권한(Role) 기반 접근 제어

특정 API 호출 시 사용자 역할(Role) 확인.
Spring Security에서 JWT 검증
Spring Security에서는 JwtDecoder를 사용하여 토큰을 검증할 수 있다.
이제 JWT 검증을 수행하는 JwtTokenVerifier 필터를 작성해보자.

@Component
public class JwtTokenVerifier extends OncePerRequestFilter {

    private final JwtDecoder jwtDecoder;

    public JwtTokenVerifier(JwtDecoder jwtDecoder) {
        this.jwtDecoder = jwtDecoder;
    }

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)
            throws ServletException, IOException {
        String authorizationHeader = request.getHeader("Authorization");

        if (authorizationHeader == null || !authorizationHeader.startsWith("Bearer ")) {
            filterChain.doFilter(request, response);
            return;
        }

        String token = authorizationHeader.replace("Bearer ", "");

        try {
            Jwt jwt = jwtDecoder.decode(token);
            String username = jwt.getSubject();
            List<SimpleGrantedAuthority> authorities = extractRoles(jwt);

            Authentication authentication = new UsernamePasswordAuthenticationToken(username, null, authorities);
            SecurityContextHolder.getContext().setAuthentication(authentication);
        } catch (JwtException e) {
            response.setStatus(HttpServletResponse.SC_UNAUTHORIZED);
            return;
        }

        filterChain.doFilter(request, response);
    }

    private List<SimpleGrantedAuthority> extractRoles(Jwt jwt) {
        List<String> roles = jwt.getClaim("roles");
        return roles.stream()
                .map(SimpleGrantedAuthority::new)
                .collect(Collectors.toList());
    }
}
코드 설명
doFilterInternal(): 요청이 들어올 때마다 Authorization 헤더를 확인하고 JWT를 검증.
jwtDecoder.decode(token): JWT를 디코딩하여 서명 검증 및 만료 여부 확인.
extractRoles(): roles 클레임에서 사용자 권한 정보를 추출.
SecurityContextHolder.getContext().setAuthentication(authentication): 인증 정보를 Spring Security의 컨텍스트에 저장.
JWT 검증을 위한 Security 설정
위에서 작성한 JwtTokenVerifier 필터를 Spring Security 설정에 추가해야 한다.

@Configuration
@EnableWebSecurity
public class SecurityConfig {

    private final JwtTokenVerifier jwtTokenVerifier;

    public SecurityConfig(JwtTokenVerifier jwtTokenVerifier) {
        this.jwtTokenVerifier = jwtTokenVerifier;
    }

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        return http
                .csrf().disable()
                .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS)
                .authorizeHttpRequests(auth -> auth
                        .requestMatchers("/auth/login").permitAll()
                        .anyRequest().authenticated()
                )
                .addFilterBefore(jwtTokenVerifier, UsernamePasswordAuthenticationFilter.class)
                .build();
    }
}
Security 설정 코드 설명
.csrf().disable(): CSRF 보호를 비활성화 (JWT는 상태를 유지하지 않기 때문).
.sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS): 세션을 사용하지 않는 방식으로 설정.
.authorizeHttpRequests():
/auth/login은 모든 사용자 접근 가능.
그 외 요청은 JWT 인증이 필요.
.addFilterBefore(jwtTokenVerifier, UsernamePasswordAuthenticationFilter.class):
JWT 검증 필터를 UsernamePasswordAuthenticationFilter 이전에 실행하도록 설정.
JWT 검증 실패 시 처리
JWT가 유효하지 않은 경우, 예외 처리 로직을 추가하여 적절한 응답을 반환해야 한다.
예를 들어, 유효하지 않은 JWT가 감지되었을 때 401 Unauthorized 응답을 반환하는 필터를 작성할 수 있다.

@Component
public class JwtExceptionHandlerFilter extends OncePerRequestFilter {

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)
            throws ServletException, IOException {
        try {
            filterChain.doFilter(request, response);
        } catch (JwtException e) {
            response.setStatus(HttpServletResponse.SC_UNAUTHORIZED);
            response.getWriter().write("Invalid JWT Token");
            response.getWriter().flush();
        }
    }
}
Security 설정에서 추가 적용

.addFilterBefore(new JwtExceptionHandlerFilter(), JwtTokenVerifier.class)
JWT 검증 후 사용자 권한(Role) 활용
Spring Security의 @PreAuthorize 또는 @Secured를 사용하여 JWT를 기반으로 API 접근을 제어할 수 있다.

@RestController
@RequestMapping("/admin")
public class AdminController {

    @PreAuthorize("hasRole('ADMIN')")
    @GetMapping("/dashboard")
    public ResponseEntity<String> getAdminDashboard() {
        return ResponseEntity.ok("Admin Dashboard Access Granted");
    }
}
@PreAuthorize("hasRole('ADMIN')"): JWT의 역할(Role) 정보를 확인하여 API 접근을 제한.
JWT 검증 후 인증된 사용자 정보 조회
JWT 검증 후 인증된 사용자 정보를 컨트롤러에서 가져올 수도 있다.

@RestController
@RequestMapping("/user")
public class UserController {

    @GetMapping("/profile")
    public ResponseEntity<String> getUserProfile(Authentication authentication) {
        return ResponseEntity.ok("Hello, " + authentication.getName());
    }
}
authentication.getName(): 현재 로그인한 사용자의 ID 반환.
실습 문제
문제 1: JWT를 검증하는 필터 구현
아래 요구사항을 만족하는 코드를 작성하시오.

HTTP 요청의 Authorization 헤더에서 JWT를 추출한다.
JWT를 검증하고, 유효한 경우 사용자 정보를 SecurityContext에 저장한다.
검증 실패 시 401 Unauthorized 응답을 반환한다.
문제 2: JWT를 활용한 사용자 인증 API 구현
다음 요구사항을 만족하는 코드를 작성하시오.

사용자가 로그인하면 JWT를 발급하여 클라이언트에 반환한다.
클라이언트가 JWT를 포함하여 API 요청을 하면, 서버는 이를 검증하고 사용자 정보를 반환한다.
만료된 JWT일 경우 403 Forbidden 응답을 반환한다.
5.3. Refresh Token을 활용한 Access Token 갱신
Refresh Token은 OAuth2와 JWT 기반의 인증 시스템에서 Access Token을 재발급하는 데 사용된다.
이 절에서는 Refresh Token을 이용해 Access Token을 갱신하는 방식과 보안적으로 안전하게 다루는 방법을 설명한다.

Refresh Token의 필요성
Access Token은 보안상의 이유로 유효 기간이 짧게 설정된다.
만약 Access Token이 만료될 때마다 사용자가 다시 로그인해야 한다면 매우 불편할 것이다.
이를 해결하기 위해 Refresh Token을 사용하여 새로운 Access Token을 발급받는다.

Refresh Token의 주요 역할

Access Token 만료 시 새로운 Access Token을 발급
→ 사용자는 다시 로그인하지 않아도 된다.
Access Token보다 긴 수명을 가짐
→ 일반적으로 Access Token은 15~30분, Refresh Token은 7일~30일 정도로 설정.
보안 강화를 위해 서버에서만 검증 가능
→ Refresh Token은 클라이언트가 직접 검증할 수 없으며, 반드시 서버를 거쳐야 한다.
Refresh Token 기반 인증 흐름
Refresh Token을 활용한 인증 과정은 다음과 같다.

사용자가 로그인을 하면 Access Token과 Refresh Token을 함께 발급받는다.
클라이언트는 Access Token을 사용하여 API 요청을 보낸다.
Access Token이 만료되면 Refresh Token을 사용하여 새로운 Access Token을 요청한다.
서버는 Refresh Token을 검증한 후 새로운 Access Token을 생성하여 클라이언트에 반환한다.
흐름 예시

[STEP 1] 사용자가 로그인 → 서버가 Access Token & Refresh Token 발급
[STEP 2] 클라이언트가 Access Token으로 API 요청
[STEP 3] Access Token 만료 시 → Refresh Token을 사용해 새로운 Access Token 요청
[STEP 4] 서버가 Refresh Token 검증 후 새로운 Access Token 발급
[STEP 5] 클라이언트는 새로운 Access Token을 사용해 API 요청 계속 수행
Refresh Token 발급 및 저장 방식
Refresh Token을 안전하게 관리하는 것이 중요하다.
보통 다음 두 가지 방식이 있다.

Refresh Token을 데이터베이스(DB)에 저장

Refresh Token을 사용자별로 데이터베이스에 저장하고 관리.
보안이 강화되지만, 추가적인 DB 조회 부담이 있음.
Refresh Token을 Redis에 저장

Redis를 이용하여 유효 기간이 있는 Refresh Token을 저장.
빠른 조회가 가능하고, TTL(Time-To-Live)을 설정할 수 있음.
Refresh Token을 이용한 Access Token 갱신 API 구현
다음은 Spring Boot + Spring Security를 이용하여 Refresh Token을 활용한 Access Token 갱신 API를 구현하는 예제이다.

1. Refresh Token을 포함한 JWT 발급

public class JwtTokenProvider {

    private final String secretKey = "mySecretKey"; // 서명 키
    private final long accessTokenValidity = 1000 * 60 * 30; // 30분
    private final long refreshTokenValidity = 1000 * 60 * 60 * 24 * 7; // 7일

    public String generateAccessToken(String username, List<String> roles) {
        return Jwts.builder()
                .setSubject(username)
                .claim("roles", roles)
                .setIssuedAt(new Date())
                .setExpiration(new Date(System.currentTimeMillis() + accessTokenValidity))
                .signWith(SignatureAlgorithm.HS256, secretKey)
                .compact();
    }

    public String generateRefreshToken(String username) {
        return Jwts.builder()
                .setSubject(username)
                .setIssuedAt(new Date())
                .setExpiration(new Date(System.currentTimeMillis() + refreshTokenValidity))
                .signWith(SignatureAlgorithm.HS256, secretKey)
                .compact();
    }
}
generateAccessToken(): 30분짜리 Access Token 생성.
generateRefreshToken(): 7일짜리 Refresh Token 생성.
2. Refresh Token 저장 및 관리
Refresh Token을 데이터베이스 또는 Redis에 저장하여 관리할 수 있다.
아래는 Refresh Token을 MySQL에 저장하는 방식이다.

@Entity
public class RefreshToken {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String username;
    private String refreshToken;
    private Date expiryDate;

    // Getter, Setter
}
@Repository
public interface RefreshTokenRepository extends JpaRepository<RefreshToken, Long> {
    Optional<RefreshToken> findByRefreshToken(String refreshToken);
}
RefreshTokenRepository: Refresh Token을 데이터베이스에서 조회하는 JPA 인터페이스.
3. Refresh Token을 이용한 Access Token 갱신 API
사용자가 Access Token을 갱신하는 API를 만든다.

@RestController
@RequestMapping("/auth")
public class AuthController {

    private final JwtTokenProvider jwtTokenProvider;
    private final RefreshTokenRepository refreshTokenRepository;

    public AuthController(JwtTokenProvider jwtTokenProvider, RefreshTokenRepository refreshTokenRepository) {
        this.jwtTokenProvider = jwtTokenProvider;
        this.refreshTokenRepository = refreshTokenRepository;
    }

    @PostMapping("/refresh")
    public ResponseEntity<?> refreshAccessToken(@RequestBody Map<String, String> request) {
        String refreshToken = request.get("refreshToken");

        Optional<RefreshToken> storedToken = refreshTokenRepository.findByRefreshToken(refreshToken);
        if (storedToken.isEmpty()) {
            return ResponseEntity.status(HttpStatus.UNAUTHORIZED).body("Invalid Refresh Token");
        }

        String newAccessToken = jwtTokenProvider.generateAccessToken(storedToken.get().getUsername(), List.of("USER"));
        return ResponseEntity.ok(Map.of("accessToken", newAccessToken));
    }
}
4. 클라이언트 요청 예시
클라이언트가 새로운 Access Token을 요청할 때, 다음과 같이 요청을 보낸다.

Request

POST /auth/refresh
Content-Type: application/json

{
  "refreshToken": "eyJhbGciOiJIUzI1..."
}
Response

{
  "accessToken": "eyJhbGciOiJIUzI1..."
}
클라이언트는 새로운 Access Token을 받아 API 요청을 계속 수행할 수 있다.
Refresh Token 보안 고려 사항
Refresh Token은 절대 클라이언트에서 노출되지 않도록 해야 한다.

로컬 스토리지(예: localStorage)에 저장하면 보안 취약점이 발생할 수 있음.
안전한 HTTP-Only 쿠키에 저장하는 것이 권장됨.
Refresh Token 유효 기간을 설정하고 만료 시 재로그인 요구

Refresh Token이 너무 길면 보안상 위험이 크므로, 적절한 유효 기간을 설정해야 한다.
Refresh Token을 재사용할 경우 이를 무효화해야 한다.

사용된 Refresh Token을 즉시 데이터베이스에서 삭제하여 동일한 토큰이 여러 번 사용되지 않도록 한다.
Refresh Token의 탈취를 방지하기 위해 IP 및 기기 정보를 검증

발급 시 사용자의 IP, User-Agent 정보를 저장하고, 이후 요청이 들어올 때 일치 여부를 확인한다.
실습 문제
문제 1: Refresh Token을 활용한 JWT 갱신
아래 요구사항을 만족하는 코드를 작성하시오.

사용자가 로그인을 하면 Access Token과 Refresh Token을 함께 발급한다.
클라이언트는 Access Token이 만료될 경우, Refresh Token을 이용하여 새로운 Access Token을 요청할 수 있다.
Refresh Token이 유효한 경우 새로운 Access Token을 발급하여 반환한다.
문제 2: Refresh Token 저장 및 보안 처리
다음 요구사항을 만족하는 코드를 작성하시오.

Refresh Token을 안전하게 저장하기 위해 데이터베이스 또는 Redis를 활용한다.
사용자가 로그아웃하면 해당 사용자의 Refresh Token을 삭제한다.
Refresh Token이 만료되었을 경우, 새로운 토큰을 요청할 수 없도록 한다.
6. OAuth2 + JWT를 활용한 SSO 구현
6.1. SSO(Single Sign-On) 개요
SSO(Single Sign-On, 단일 로그인)는 한 번의 로그인으로 여러 애플리케이션 또는 서비스에 접근할 수 있도록 하는 인증 방식이다.
OAuth2와 JWT를 활용하면 분산된 서비스 간에 인증 정보를 공유하면서 보안을 유지하는 SSO 시스템을 구축할 수 있다.

SSO의 필요성
현대적인 웹 애플리케이션과 기업 환경에서는 여러 개의 독립적인 서비스(예: 메인 웹사이트, API 서버, 관리자 페이지 등) 를 운영한다.
각각의 서비스마다 개별 로그인 시스템을 운영하면 사용자 경험이 불편하고, 보안 관리가 어려워진다.
SSO는 이런 문제를 해결할 수 있도록 하나의 인증 절차로 여러 서비스에 접근할 수 있게 한다.

SSO를 적용할 경우 얻을 수 있는 장점

사용자 편의성 증가
한 번 로그인하면 모든 관련 서비스에 자동 로그인.
보안 강화
여러 서비스에서 같은 로그인 정보를 공유하지 않으므로 비밀번호 관리가 용이.
관리 비용 절감
각 서비스에서 별도의 인증 시스템을 구현할 필요 없이 중앙 인증 서버를 활용.
OAuth2와 JWT를 활용한 SSO 구조
OAuth2와 JWT를 기반으로 SSO를 구현하면, 중앙 인증 서버에서 로그인 정보를 검증하고 JWT를 사용하여 각 서비스에 인증 정보를 전달할 수 있다.

SSO 시스템의 핵심 구성 요소

Authentication Server (인증 서버)
사용자의 로그인 요청을 처리하고, JWT를 발급하는 역할.
OAuth2 Authorization Server로 동작하며, 인증이 성공하면 Access Token(JWT) 를 발급.
Client Applications (클라이언트 애플리케이션)
인증 서버에서 발급한 JWT를 이용하여 보호된 리소스에 접근.
REST API 서버, 웹 애플리케이션, 모바일 앱 등이 포함됨.
Resource Server (리소스 서버)
JWT를 검증하고 사용자 요청을 처리하는 서버.
사용자가 요청을 보낼 때 JWT를 포함하면, 이를 검증하여 접근을 허용.
OAuth2 + JWT 기반 SSO 인증 흐름
OAuth2와 JWT를 활용한 SSO 시스템에서는 다음과 같은 인증 절차가 수행된다.

사용자가 로그인 페이지에서 아이디/비밀번호 입력 후 인증 요청
인증 서버(Authentication Server) 가 로그인 정보를 검증
검증 성공 시 JWT 기반 Access Token과 Refresh Token 발급
클라이언트 애플리케이션(Client App)이 발급받은 JWT를 저장
사용자가 리소스 서버(Resource Server)에 요청을 보낼 때 JWT를 포함
리소스 서버는 JWT를 검증 후 사용자 요청을 처리
Access Token이 만료되면, Refresh Token을 이용하여 새로운 Access Token을 발급받음
SSO 인증 흐름 예시

[STEP 1] 사용자가 로그인 요청 → 인증 서버에서 검증
[STEP 2] 인증 서버가 JWT 기반 Access Token & Refresh Token 발급
[STEP 3] 클라이언트가 Access Token을 저장하고, API 요청 시 포함
[STEP 4] 리소스 서버는 Access Token을 검증하여 요청 처리
[STEP 5] Access Token이 만료되면, Refresh Token을 이용하여 새로운 Access Token 요청
[STEP 6] 인증 서버가 Refresh Token 검증 후 새로운 Access Token 발급
OAuth2와 JWT를 활용한 SSO 인증 서버 구현
이제 Spring Boot + Spring Security를 사용하여 OAuth2 기반 SSO 인증 서버를 구현한다.

1. 의존성 추가 (pom.xml)

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-oauth2-authorization-server</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
spring-boot-starter-oauth2-authorization-server: OAuth2 인증 서버 구현을 위한 필수 라이브러리.
spring-boot-starter-security: Spring Security를 활용한 보안 설정.
spring-boot-starter-web: REST API를 제공하기 위한 웹 애플리케이션 기능.
2. OAuth2 인증 서버 설정
Spring Security를 사용하여 OAuth2 인증 서버를 설정한다.

@Configuration
@EnableAuthorizationServer
public class OAuth2AuthorizationServerConfig extends AuthorizationServerConfigurerAdapter {

    @Override
    public void configure(ClientDetailsServiceConfigurer clients) throws Exception {
        clients.inMemory()
            .withClient("client-id")
            .secret("{noop}client-secret")
            .authorizedGrantTypes("authorization_code", "refresh_token", "password")
            .scopes("read", "write")
            .accessTokenValiditySeconds(900)  // 15분
            .refreshTokenValiditySeconds(604800); // 7일
    }

    @Override
    public void configure(AuthorizationServerSecurityConfigurer security) {
        security.tokenKeyAccess("permitAll()")
                .checkTokenAccess("isAuthenticated()");
    }
}
Client 설정: 클라이언트 애플리케이션이 OAuth2 인증을 요청할 수 있도록 설정.
Access Token 만료 시간: 15분으로 설정.
Refresh Token 만료 시간: 7일로 설정.
3. JWT 기반 Access Token 발급
OAuth2 인증 서버에서 JWT를 활용하여 Access Token을 발급하는 설정을 추가한다.

@Configuration
public class JwtTokenConfig {

    private final String secretKey = "mySecretKey";

    public String generateJwtToken(Authentication authentication) {
        return Jwts.builder()
                .setSubject(authentication.getName())
                .setIssuedAt(new Date())
                .setExpiration(new Date(System.currentTimeMillis() + 900000)) // 15분
                .signWith(SignatureAlgorithm.HS256, secretKey)
                .compact();
    }
}
사용자가 로그인하면 JWT 기반 Access Token이 발급된다.
setExpiration()을 통해 Access Token의 유효 시간을 15분으로 설정.
4. 리소스 서버에서 JWT 검증
리소스 서버는 클라이언트가 요청한 JWT를 검증하여 사용자를 인증한다.

@Configuration
@EnableResourceServer
public class ResourceServerConfig extends ResourceServerConfigurerAdapter {

    @Override
    public void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
            .antMatchers("/public").permitAll()
            .antMatchers("/user").authenticated();
    }
}
/public: 인증 없이 접근 가능.
/user: JWT가 있어야 접근 가능.
SSO 구현 시 고려할 보안 사항
JWT 탈취 방지

HTTPS를 반드시 사용하여 네트워크에서 토큰이 노출되지 않도록 한다.
JWT는 브라우저의 localStorage보다는 HTTP-Only 쿠키에 저장하는 것이 보안상 더 안전하다.
Refresh Token 보안 강화

Refresh Token이 탈취되면 지속적으로 새로운 Access Token을 발급받을 수 있으므로, DB 또는 Redis에서 관리해야 한다.
Refresh Token을 재사용할 수 없도록, 한 번 사용되면 폐기하는 방식을 적용하는 것이 보안적으로 유리하다.
사용자 로그아웃 처리

로그아웃 시 Refresh Token을 무효화하고, Access Token을 폐기해야 한다.
학습자의 사고를 돕기 위한 질문
SSO(Single Sign-On)의 개념은 무엇이며, 기업 환경에서 어떤 장점을 제공하는가?

하나의 로그인으로 여러 애플리케이션에 접근하는 방식에 대해 생각해보라.
OAuth2와 JWT를 활용한 SSO 구현 시, 각 구성 요소는 어떤 역할을 하는가?

인증 서버와 리소스 서버의 역할을 고려해보라.
6.2. OAuth2 기반의 SSO 구현
OAuth2 기반 SSO(Single Sign-On) 시스템을 구축하면, 여러 애플리케이션에서 단일한 인증을 통해 접근이 가능하도록 만들 수 있다.
이를 구현하기 위해 OAuth2 인증 서버를 설정하고, 클라이언트 애플리케이션들이 이를 통해 인증 및 권한을 위임받도록 구성한다.

OAuth2 기반 SSO 시스템의 개념
OAuth2를 기반으로 한 SSO는 중앙 인증 서버(Authorization Server) 가 인증을 처리하고,
각 애플리케이션(Client Applications)이 인증된 사용자를 식별할 수 있도록 Access Token과 Refresh Token을 발급하는 방식으로 동작한다.

이 방식의 가장 큰 장점은 여러 개의 독립적인 애플리케이션에서 동일한 인증 정보를 사용할 수 있다는 것이다.
즉, 사용자가 한 번 로그인하면 다른 모든 서비스에서도 자동으로 로그인된 상태를 유지할 수 있다.

OAuth2 SSO 인증 흐름
사용자가 SSO 로그인 페이지에서 아이디와 비밀번호 입력.
OAuth2 인증 서버가 사용자를 인증하고, JWT 기반 Access Token과 Refresh Token을 발급.
사용자가 Client Application(웹 또는 모바일 애플리케이션)에 접근.
클라이언트 애플리케이션이 발급받은 Access Token을 사용하여 API 요청.
리소스 서버(Resource Server)는 Access Token을 검증하여 요청을 처리.
Access Token이 만료되면, Refresh Token을 이용하여 새로운 Access Token을 발급.
사용자 → [로그인 요청] → OAuth2 인증 서버
OAuth2 인증 서버 → [Access Token, Refresh Token 발급] → 클라이언트 애플리케이션
클라이언트 애플리케이션 → [Access Token 포함하여 API 요청] → 리소스 서버
리소스 서버 → [Access Token 검증 후 응답 반환]
Access Token 만료 시 → [Refresh Token을 사용하여 새로운 Access Token 발급]
OAuth2 SSO 구현: Spring Security 설정
OAuth2 기반의 SSO를 구현하기 위해 Spring Security와 Spring Authorization Server를 활용하여 인증 서버를 설정할 수 있다.

1. OAuth2 인증 서버(Authorization Server) 설정

@Configuration
@EnableAuthorizationServer
public class AuthorizationServerConfig extends AuthorizationServerConfigurerAdapter {

    @Override
    public void configure(ClientDetailsServiceConfigurer clients) throws Exception {
        clients.inMemory()
            .withClient("sso-client")
            .secret("{noop}client-secret")
            .authorizedGrantTypes("authorization_code", "refresh_token", "password")
            .scopes("read", "write")
            .accessTokenValiditySeconds(900)  // Access Token 15분 유지
            .refreshTokenValiditySeconds(604800); // Refresh Token 7일 유지
    }

    @Override
    public void configure(AuthorizationServerSecurityConfigurer security) {
        security.tokenKeyAccess("permitAll()")
                .checkTokenAccess("isAuthenticated()");
    }
}
withClient("sso-client"): OAuth2 Client 등록 (SSO를 사용할 애플리케이션).
authorizedGrantTypes("authorization_code", "refresh_token", "password"): 다양한 인증 방식을 지원.
accessTokenValiditySeconds(900): Access Token의 유효 시간(15분).
refreshTokenValiditySeconds(604800): Refresh Token의 유효 시간(7일).
2. 클라이언트 애플리케이션(Client Application) 설정
클라이언트 애플리케이션에서 OAuth2 기반의 SSO를 적용하려면,
Spring Security와 OAuth2 Client를 활용하여 인증 요청을 처리해야 한다.

@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/public").permitAll()
                .antMatchers("/user").authenticated()
            .and()
            .oauth2Login(); // OAuth2 기반 로그인 활성화
    }
}
/public 경로는 누구나 접근 가능.
/user 경로는 인증된 사용자만 접근 가능.
.oauth2Login()을 통해 OAuth2 로그인 설정.
3. JWT 기반 Access Token과 Refresh Token 발급
OAuth2 인증 서버에서 JWT 기반의 Access Token을 발급할 수 있도록 설정을 추가한다.

@Configuration
public class JwtTokenConfig {

    private final String secretKey = "mySecretKey";

    public String generateJwtToken(Authentication authentication) {
        return Jwts.builder()
                .setSubject(authentication.getName())
                .setIssuedAt(new Date())
                .setExpiration(new Date(System.currentTimeMillis() + 900000)) // 15분
                .signWith(SignatureAlgorithm.HS256, secretKey)
                .compact();
    }
}
Access Token의 만료 시간은 15분으로 설정.
HS256 알고리즘을 사용하여 JWT 서명(Signature) 생성.
4. 리소스 서버(Resource Server) 설정
OAuth2 SSO를 사용하는 클라이언트 애플리케이션이 API를 요청할 때,
리소스 서버(Resource Server)는 Access Token을 검증하여 요청을 처리해야 한다.

@Configuration
@EnableResourceServer
public class ResourceServerConfig extends ResourceServerConfigurerAdapter {

    @Override
    public void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
            .antMatchers("/public").permitAll()
            .antMatchers("/user").authenticated();
    }
}
/public: 인증 없이 접근 가능.
/user: JWT 기반 Access Token을 포함해야 접근 가능.
OAuth2 SSO 환경에서의 사용자 인증 흐름
사용자가 https://sso.example.com/login에서 로그인 요청.
OAuth2 인증 서버가 사용자 정보를 검증하고 Access Token을 발급.
사용자는 https://client-app.example.com에서 API 요청을 수행.
클라이언트 애플리케이션은 Access Token을 포함하여 리소스 서버에 요청.
리소스 서버가 Access Token을 검증하고 요청을 처리.
OAuth2 기반 SSO 적용 시 고려해야 할 보안 요소
Access Token의 유효 시간을 짧게 설정

일반적으로 15~30분 사이로 설정하며, Refresh Token을 활용하여 갱신.
Refresh Token 저장 방식

Refresh Token이 탈취되면 장기적으로 Access Token을 계속 갱신할 수 있음.
따라서, Refresh Token은 DB 또는 Redis에서 관리하는 것이 보안상 안전.
HTTPS 사용

OAuth2 인증 과정과 JWT 전송 시 HTTPS를 강제 적용해야 한다.
사용자 로그아웃 처리

로그아웃 시 Refresh Token을 즉시 무효화해야 하며,
Access Token은 서버 측에서 블랙리스트 처리하는 방식이 필요.
실습 문제
문제 1: OAuth2 기반의 SSO 로그인 구현
아래 요구사항을 만족하는 코드를 작성하시오.

OAuth2 인증 서버를 구현하여 사용자 로그인을 처리한다.
클라이언트 애플리케이션이 OAuth2 인증 서버로부터 Access Token을 받아야 한다.
발급된 토큰을 사용하여 다른 서비스에도 접근 가능하도록 한다.
문제 2: OAuth2 SSO를 활용한 사용자 프로필 정보 조회
다음 요구사항을 만족하는 코드를 작성하시오.

클라이언트가 OAuth2 인증 서버로부터 Access Token을 받아 로그인한다.
사용자가 로그인 후, 토큰을 이용하여 프로필 정보를 요청할 수 있도록 API를 구현한다.
사용자의 이름, 이메일, 권한(role) 정보를 JSON 형식으로 반환한다.
6.3. SSO 환경에서의 보안 고려 사항
OAuth2 기반 SSO(Single Sign-On)를 구축하는 과정에서 가장 중요한 요소 중 하나는 보안이다.
SSO 시스템은 여러 애플리케이션에서 공유되므로, 하나의 보안 취약점이 전체 시스템에 영향을 미칠 수 있다.
따라서 토큰 관리, 사용자 인증 보안, 네트워크 보안 등을 철저하게 고려해야 한다.

SSO 환경에서 발생할 수 있는 보안 위협
SSO 환경에서는 일반적인 인증 시스템보다 보안 위협이 크다.
특히 다음과 같은 보안 취약점을 방지해야 한다.

Access Token 탈취 및 재사용 공격

악의적인 사용자가 Access Token을 탈취하면 해당 사용자의 권한을 도용할 수 있음.
Refresh Token 도난

Refresh Token은 긴 유효 기간을 가지므로 탈취될 경우 장기적으로 사용 가능.
Token Replay Attack(재사용 공격)

공격자가 이전에 사용된 토큰을 복사하여 요청을 반복 실행.
Authorization Code Interception

OAuth2 인증 과정에서 Authorization Code를 가로채어 악용하는 공격.
Session Fixation 공격

세션이 탈취당하면 사용자의 인증 정보가 그대로 유지됨.
Cross-Site Request Forgery (CSRF)

사용자의 인증 정보를 조작하여 의도하지 않은 요청을 발생시키는 공격.
이러한 위협을 방지하기 위해, SSO 환경에서 철저한 보안 고려 사항을 적용해야 한다.

Access Token과 Refresh Token 보안 관리
SSO 환경에서는 Access Token과 Refresh Token을 안전하게 저장하고 관리하는 것이 중요하다.
다음과 같은 전략을 적용하여 보안을 강화할 수 있다.

1. Access Token의 유효 기간을 짧게 설정

일반적으로 Access Token의 만료 시간을 5~30분으로 설정한다.
유효 기간이 짧을수록 토큰이 탈취되었을 때 피해를 최소화할 수 있다.
.withClient("sso-client")
    .secret("{noop}client-secret")
    .authorizedGrantTypes("authorization_code", "refresh_token", "password")
    .scopes("read", "write")
    .accessTokenValiditySeconds(900)  // Access Token 15분 유지
    .refreshTokenValiditySeconds(604800); // Refresh Token 7일 유지
2. Refresh Token 저장 방식

Refresh Token은 서버에서 안전하게 관리해야 하며, 클라이언트가 보관하면 안 됨.
Database 또는 Redis에 저장하여 필요한 경우만 검증하도록 설정.
@Configuration
public class RefreshTokenStorage {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    public void storeRefreshToken(String refreshToken, String userId) {
        jdbcTemplate.update("INSERT INTO refresh_tokens (user_id, token) VALUES (?, ?)", userId, refreshToken);
    }

    public boolean validateRefreshToken(String refreshToken, String userId) {
        return jdbcTemplate.queryForObject(
            "SELECT COUNT(*) FROM refresh_tokens WHERE user_id = ? AND token = ?",
            Integer.class, userId, refreshToken) > 0;
    }
}
Refresh Token을 저장하고 검증하는 로직을 DB에서 수행.
탈취된 Refresh Token이 무효화될 수 있도록 관리.
Token Replay Attack 방지 (토큰 재사용 공격 방지)
토큰 재사용 공격(Token Replay Attack)은 공격자가 유효한 토큰을 가로채서 동일한 요청을 반복 실행하는 공격이다.
이를 방지하기 위해 JWT에 Nonce(일회성 값) 또는 JTI(JWT ID)를 추가하여 중복된 토큰을 차단할 수 있다.

1. JWT에 JTI 추가하기

JTI(JWT ID)는 JWT의 고유 식별자로, 중복된 토큰을 방지하는 데 사용된다.
public String generateJwtToken(Authentication authentication) {
    return Jwts.builder()
            .setSubject(authentication.getName())
            .setIssuedAt(new Date())
            .setExpiration(new Date(System.currentTimeMillis() + 900000)) // 15분
            .setId(UUID.randomUUID().toString()) // JTI 추가
            .signWith(SignatureAlgorithm.HS256, secretKey)
            .compact();
}
2. 블랙리스트 기반 토큰 관리

JWT가 유효하더라도 이미 사용된 토큰인지 확인하기 위해 서버에서 사용된 토큰을 추적.
private Set<String> usedTokens = new HashSet<>();

public boolean isTokenUsed(String jti) {
    return usedTokens.contains(jti);
}

public void markTokenAsUsed(String jti) {
    usedTokens.add(jti);
}
JTI를 서버에 저장하고, 이미 사용된 JTI는 차단.
Authorization Code Interception 방지
OAuth2의 Authorization Code Flow에서 Authorization Code를 가로채는 공격을 방지하려면,
PKCE (Proof Key for Code Exchange) 메커니즘을 적용해야 한다.

PKCE 적용
PKCE는 Code Challenge(난수 기반 인코딩 값)과 Code Verifier(검증 코드) 를 사용하여 Authorization Code 탈취를 방지한다.
public String generateCodeVerifier() {
    byte[] randomBytes = new byte[32];
    new SecureRandom().nextBytes(randomBytes);
    return Base64.getUrlEncoder().withoutPadding().encodeToString(randomBytes);
}

public String generateCodeChallenge(String codeVerifier) {
    return Base64.getUrlEncoder().withoutPadding().encodeToString(
        MessageDigest.getInstance("SHA-256").digest(codeVerifier.getBytes(StandardCharsets.UTF_8)));
}
OAuth2 요청 시 PKCE 적용
클라이언트가 Authorization Code 요청을 보낼 때, Code Challenge를 함께 전송.
GET /oauth/authorize?
  response_type=code&
  client_id=sso-client&
  redirect_uri=https://client-app.example.com/callback&
  code_challenge=abcdefg&
  code_challenge_method=S256
Authorization Server에서 Code Verifier 검증
토큰 요청 시 Code Verifier가 일치하는지 확인하여 Authorization Code 탈취를 방지.
Cross-Site Request Forgery (CSRF) 방지
OAuth2와 JWT 기반 인증에서는 CSRF(Cross-Site Request Forgery) 공격을 방지해야 한다.
특히, 클라이언트가 Access Token을 로컬 스토리지에 저장하면 공격자가 이를 탈취할 수 있음.

Access Token을 HTTP-Only 쿠키에 저장
JavaScript가 접근할 수 없도록 HTTP-Only, Secure 쿠키를 설정.
ResponseCookie cookie = ResponseCookie.from("access_token", jwt)
        .httpOnly(true)
        .secure(true)
        .path("/")
        .maxAge(Duration.ofMinutes(15))
        .build();
response.addHeader("Set-Cookie", cookie.toString());
CORS 정책 강화
OAuth2 기반 SSO에서는 CORS 설정을 철저하게 구성해야 한다.
@Configuration
public class CorsConfig {
    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/**")
                        .allowedOrigins("https://client-app.example.com")
                        .allowedMethods("GET", "POST", "PUT", "DELETE")
                        .allowCredentials(true);
            }
        };
    }
}
학습자의 사고를 돕기 위한 질문
SSO 환경에서 보안 위협이 발생할 가능성이 높은 영역은 어디인가?

토큰 유출, 세션 하이재킹 등과 관련된 보안 위협을 고려해보라.
OAuth2 기반 SSO에서 보안 강화를 위해 적용할 수 있는 방안에는 무엇이 있는가?

Refresh Token 관리 및 만료 정책, HTTPS 적용 등을 생각해보라.
7. OAuth2와 JWT 사용 시 보안 고려 사항 및 Best Practices
7.1. OAuth2와 JWT의 보안 취약점
OAuth2와 JWT 기반 인증을 사용할 때, 다양한 보안 위협이 존재한다.
OAuth2는 권한 부여(Authorization) 를 다루는 프레임워크이며, JWT는 인증(Authentication) 및 정보 전달을 위한 토큰이다.
이 두 가지를 결합하여 인증 및 권한 부여를 수행할 때 다음과 같은 보안 취약점을 고려해야 한다.

OAuth2의 보안 취약점
토큰 탈취(Token Hijacking)

OAuth2는 액세스 토큰을 기반으로 인증을 수행하는데, 토큰이 탈취되면 공격자가 정상 사용자로 위장할 수 있다.
특히, 공유 네트워크에서 액세스 토큰이 노출될 가능성이 있다.
Authorization Code Interception

OAuth2의 authorization_code 플로우에서는 클라이언트와 인증 서버 간 Authorization Code가 전송된다.
이 과정에서 중간자 공격(Man-in-the-Middle, MITM)이 발생할 경우, 공격자가 Authorization Code를 가로챌 수 있다.
이후 공격자가 자신의 클라이언트 ID를 사용하여 Access Token을 발급받을 수 있음.
Token Replay Attack(토큰 재사용 공격)

OAuth2 기반 인증에서는 클라이언트가 한 번 발급받은 토큰을 여러 번 사용할 수 있다.
공격자가 유효한 토큰을 가로채면, 재사용하여 API 요청을 수행할 수 있음.
CSRF(Cross-Site Request Forgery)

OAuth2 로그인 과정에서 사용자가 악성 웹사이트를 방문했을 때, 자동으로 OAuth 요청이 수행될 가능성이 있다.
예를 들어, 공격자가 https://authorization-server.com/auth?client_id=malicious-app&redirect_uri=http://attacker.com 같은 링크를 사용하면,
사용자의 동의 없이 특정 액션이 실행될 수 있음.
Client Credential Leakage

OAuth2의 client_credentials 방식에서는 클라이언트 ID와 비밀 키(client secret)를 서버가 관리해야 한다.
만약 클라이언트 비밀 키가 탈취되면, 공격자는 서버로부터 무제한으로 토큰을 발급받을 수 있다.
JWT의 보안 취약점
토큰 탈취 및 정보 노출

JWT는 서버에 저장되지 않고 클라이언트에서 보관해야 한다.
클라이언트가 로컬 스토리지(Local Storage)나 세션 스토리지(Session Storage)에 JWT를 저장하면, XSS(Cross-Site Scripting) 공격을 통해 탈취될 가능성이 높다.
JWT의 만료 시간을 적절히 설정하지 않으면 장기적인 보안 위협이 됨

JWT는 기본적으로 서버에서 유효성을 검증하기 어려움.
만료 시간이 길다면, 유출되었을 때 장기간 악용될 수 있음.
대칭 키(HMAC) 사용 시 키 유출 위험

JWT 서명 방식에는 대칭 키(HMAC) 와 비대칭 키(RSA, ECDSA) 방식이 있다.
HMAC 기반 JWT를 사용하면, 유출된 키를 통해 누구나 유효한 토큰을 생성할 수 있다.
비대칭 키(RSA) 방식은 공개 키를 통해 검증만 수행하므로, 보안성이 더 높다.
JWT의 크기 문제 및 성능 이슈

JWT는 Header, Payload, Signature로 구성되며, 정보가 많아질수록 크기가 커진다.
API 요청 시, 토큰이 너무 크면 네트워크 대역폭을 낭비하고 성능 저하를 유발할 수 있음.
OAuth2와 JWT의 취약점을 해결하는 방법
각각의 보안 취약점을 해결하기 위해 다양한 보안 메커니즘을 적용할 수 있다.

토큰 탈취 방지
Access Token의 유효 시간을 짧게 설정하고, Refresh Token을 사용하여 정기적으로 갱신.
HTTPS를 사용하여 네트워크에서 토큰이 노출되지 않도록 보호.
토큰을 HTTP-Only 쿠키에 저장하여 JavaScript에서 접근하지 못하도록 설정.
ResponseCookie accessTokenCookie = ResponseCookie.from("access_token", jwt)
        .httpOnly(true)
        .secure(true)
        .path("/")
        .maxAge(Duration.ofMinutes(15))
        .build();
response.addHeader("Set-Cookie", accessTokenCookie.toString());
Authorization Code Interception 방지
OAuth2의 PKCE(Proof Key for Code Exchange) 메커니즘 적용.
클라이언트에서 SHA-256 기반 코드 챌린지를 생성하고, 인증 서버에서 이를 검증하여, 중간자 공격을 방지.
public String generateCodeChallenge(String codeVerifier) {
    return Base64.getUrlEncoder().withoutPadding().encodeToString(
        MessageDigest.getInstance("SHA-256").digest(codeVerifier.getBytes(StandardCharsets.UTF_8)));
}
Token Replay Attack 방지
JTI(JWT ID) 및 Nonce(일회성 값)를 포함하여, 사용된 토큰을 서버에서 추적하고 재사용 방지.
서버에서 사용된 JTI를 저장하고, 동일한 JTI가 포함된 요청은 차단.
public String generateJwtToken(Authentication authentication) {
    return Jwts.builder()
            .setSubject(authentication.getName())
            .setIssuedAt(new Date())
            .setExpiration(new Date(System.currentTimeMillis() + 900000))
            .setId(UUID.randomUUID().toString()) // JTI 추가
            .signWith(SignatureAlgorithm.HS256, secretKey)
            .compact();
}
CSRF 공격 방지
OAuth2 인증 요청 시, CSRF 토큰을 검증하도록 구성.
OAuth2 요청과 함께 state 값을 포함하고, 응답 시 이를 검증.
GET /oauth/authorize?
  response_type=code&
  client_id=sso-client&
  redirect_uri=https://client-app.example.com/callback&
  state=random-generated-string
JWT 보안 강화를 위한 서명 알고리즘 선택
HMAC보다 RSA(RS256) 또는 ECDSA(ES256) 기반 서명 알고리즘을 사용하여 보안성을 높임.
KeyPair keyPair = KeyPairGenerator.getInstance("RSA").generateKeyPair();
Jwt jwt = Jwts.builder()
        .setSubject("user123")
        .signWith(keyPair.getPrivate(), SignatureAlgorithm.RS256)
        .compact();
Refresh Token 저장 및 관리
Refresh Token을 클라이언트가 직접 저장하지 않고, 서버에서 관리하도록 구성.
Refresh Token을 사용할 때마다 새로운 Access Token을 발급하고, 이전 Refresh Token을 무효화.
public void storeRefreshToken(String refreshToken, String userId) {
    jdbcTemplate.update("INSERT INTO refresh_tokens (user_id, token) VALUES (?, ?)", userId, refreshToken);
}

public boolean validateRefreshToken(String refreshToken, String userId) {
    return jdbcTemplate.queryForObject(
            "SELECT COUNT(*) FROM refresh_tokens WHERE user_id = ? AND token = ?",
            Integer.class, userId, refreshToken) > 0;
}
학습자의 사고를 돕기 위한 질문
OAuth2에서 Access Token이 유출될 경우 어떤 보안 위협이 발생할 수 있는가?

토큰 탈취로 인해 공격자가 API를 무단으로 호출할 가능성을 고려해보라.
JWT 토큰이 만료되지 않거나 너무 긴 유효 기간을 가질 경우 발생할 수 있는 보안 문제는 무엇인가?

만료되지 않는 토큰이 공격자의 손에 들어갈 경우를 생각해보라.
OAuth2에서 Authorization Code Interception 공격이란 무엇이며, 이를 방지하기 위한 방법은 무엇인가?

PKCE(Proof Key for Code Exchange)의 역할을 고려해보라.
7.2. JWT 토큰 암호화 및 서명 강화
JWT(Json Web Token)는 기본적으로 Base64 URL-safe 인코딩이 적용된 문자열로 전달되지만,
이 인코딩 자체는 보안 기능을 제공하지 않는다.
따라서 JWT의 암호화와 서명을 통해 보안을 강화할 필요가 있다.

JWT 서명(Signature) 강화
JWT는 기본적으로 서명(Signature)을 포함한 JWS(JSON Web Signature) 형식을 사용하여 무결성을 보장한다.
이 서명은 HMAC, RSA, ECDSA 등 다양한 알고리즘을 이용해 생성할 수 있으며,
이러한 서명 기법을 어떻게 적용하는지가 보안성을 결정짓는 중요한 요소다.

HMAC (Hash-based Message Authentication Code)
HMAC을 활용한 서명 방식은 서버에서 공유하는 비밀 키(Secret Key) 를 기반으로 서명을 생성한다.
서버에서 해당 비밀 키를 알고 있어야만 검증이 가능하므로,
이 키가 유출되면 누구나 서명된 JWT를 생성할 수 있다.
HMAC-SHA256 (HS256) 이 가장 널리 사용되며, 서버 간 트러스트가 높은 환경에서 유용하다.
String secretKey = "mySuperSecretKey";  // 안전한 키 저장 필요

String jwt = Jwts.builder()
        .setSubject("user123")
        .setIssuedAt(new Date())
        .setExpiration(new Date(System.currentTimeMillis() + 600000))  // 10분 후 만료
        .signWith(SignatureAlgorithm.HS256, secretKey)
        .compact();
RSA (Rivest-Shamir-Adleman)
RSA 기반의 서명 방식은 비대칭 키 암호화를 사용한다.
개인 키(Private Key)로 서명하고, 공개 키(Public Key)로 검증할 수 있으므로,
서버 간 JWT 검증이 필요한 분산 시스템에서 적합하다.
KeyPair keyPair = KeyPairGenerator.getInstance("RSA").generateKeyPair();

String jwt = Jwts.builder()
        .setSubject("user123")
        .setIssuedAt(new Date())
        .setExpiration(new Date(System.currentTimeMillis() + 600000))  // 10분 후 만료
        .signWith(keyPair.getPrivate(), SignatureAlgorithm.RS256)  // RSA 서명
        .compact();
ECDSA (Elliptic Curve Digital Signature Algorithm)
RSA보다 짧은 키 길이로 동일한 보안 수준을 제공하는 서명 방식이다.
ES256, ES384, ES512 등의 옵션이 있으며,
RSA보다 성능이 우수하고, 모바일 환경에서 활용하기에 적합하다.
KeyPair keyPair = KeyPairGenerator.getInstance("EC").generateKeyPair();

String jwt = Jwts.builder()
        .setSubject("user123")
        .setIssuedAt(new Date())
        .setExpiration(new Date(System.currentTimeMillis() + 600000))  // 10분 후 만료
        .signWith(keyPair.getPrivate(), SignatureAlgorithm.ES256)  // ECDSA 서명
        .compact();
JWT 암호화(Encryption) 적용
JWT의 기본 형태인 JWS는 서명을 통해 무결성을 보장하지만, 정보 자체를 보호하지는 않는다.
JWT의 Payload는 Base64 인코딩되어 있지만, 복호화가 필요 없는 평문(Plaintext) 데이터로 간주된다.
이 때문에 민감한 정보가 포함된 경우, 추가적인 암호화가 필요하다.
이를 해결하는 방식이 JWE(JSON Web Encryption) 이다.

JWE(JSON Web Encryption) 개요
JWE는 JWT의 내용을 암호화하여 보호하는 방식이다.
JWS처럼 서명을 통해 무결성을 보장하면서도,
Payload를 암호화하여 제3자가 내용을 확인하지 못하도록 보호할 수 있다.
일반적으로 AES 대칭 암호화 또는 RSA 공개 키 암호화를 사용한다.
JWE를 이용한 JWT 암호화 방식
AES 암호화 적용 (대칭키 방식)
AES-GCM 또는 AES-CBC 암호화를 적용하여 Payload를 보호할 수 있다.
일반적으로 JWT Payload를 AES 키로 암호화하고, 키는 별도로 관리한다.
// 암호화에 사용할 AES 키 생성
SecretKey key = Keys.secretKeyFor(SignatureAlgorithm.HS256);

String jwt = Jwts.builder()
        .setSubject("user123")
        .setIssuedAt(new Date())
        .setExpiration(new Date(System.currentTimeMillis() + 600000))
        .encryptWith(Jwts.KEY, key)  // JWE 암호화 적용
        .compact();
RSA 암호화 적용 (비대칭키 방식)
RSA를 사용하면, 공개 키(Public Key)로 암호화하고, 개인 키(Private Key)로 복호화할 수 있다.
이를 통해 토큰을 발급한 서버만이 JWT의 내용을 복호화할 수 있도록 설정 가능.
KeyPair keyPair = KeyPairGenerator.getInstance("RSA").generateKeyPair();

String jwt = Jwts.builder()
        .setSubject("user123")
        .setIssuedAt(new Date())
        .setExpiration(new Date(System.currentTimeMillis() + 600000))
        .encryptWith(Jwts.KEY, keyPair.getPublic())  // RSA 공개 키로 암호화
        .compact();
JWT 보안 강화를 위한 추가 전략
짧은 만료 시간(Expiration Time) 설정
JWT가 유출될 경우 피해를 줄이기 위해 짧은 유효 기간을 설정하는 것이 중요하다.
일반적으로 Access Token은 1030분, Refresh Token은 며칠한 달 정도로 설정한다.
String jwt = Jwts.builder()
        .setSubject("user123")
        .setIssuedAt(new Date())
        .setExpiration(new Date(System.currentTimeMillis() + 900000))  // 15분 후 만료
        .signWith(SignatureAlgorithm.HS256, secretKey)
        .compact();
토큰 무효화 및 블랙리스트 관리
JWT는 서버에서 상태를 유지하지 않는 Stateless 방식이기 때문에,
특정 토큰을 강제로 무효화하기 어렵다.
이를 해결하기 위해 토큰 블랙리스트(Blacklist)를 관리하는 방식이 필요하다.
public void revokeToken(String token) {
    jdbcTemplate.update("INSERT INTO revoked_tokens (token) VALUES (?)", token);
}

public boolean isTokenRevoked(String token) {
    return jdbcTemplate.queryForObject(
            "SELECT COUNT(*) FROM revoked_tokens WHERE token = ?", Integer.class, token) > 0;
}
Secure Cookie 또는 HTTP-Only Storage 사용
XSS 공격 방지를 위해 JWT를 HTTP-Only 쿠키에 저장하여 JavaScript에서 접근하지 못하게 한다.
SameSite 설정을 활용하여 Cross-Site 공격 방어.
ResponseCookie accessTokenCookie = ResponseCookie.from("access_token", jwt)
        .httpOnly(true)
        .secure(true)
        .sameSite("Strict")
        .path("/")
        .maxAge(Duration.ofMinutes(15))
        .build();
response.addHeader("Set-Cookie", accessTokenCookie.toString());
JWT에 최소한의 정보만 포함
필요 이상의 정보를 담으면 보안 위협이 증가하며, 토큰 크기도 커진다.
민감한 정보는 Claims에 직접 저장하는 것이 아니라, 별도의 데이터베이스에서 관리해야 한다.
7.3. Refresh Token 보안 관리 및 갱신 정책
OAuth2와 JWT 기반의 인증 시스템에서 Refresh Token은 중요한 역할을 한다.
Access Token의 유효 기간을 짧게 설정하여 보안성을 높이는 대신,
Refresh Token을 활용해 사용자의 재인증 없이 새로운 Access Token을 발급할 수 있다.
그러나 Refresh Token 자체가 유출되면 장기적인 보안 위협이 될 수 있기 때문에
안전하게 관리하고, 갱신하는 정책을 수립하는 것이 중요하다.

Refresh Token의 개념과 역할
Access Token이 만료되면 새로 발급할 수 있도록 해주는 토큰
일반적으로 장기 보관이 가능하지만, 보안적으로 신중하게 다루어야 함
Refresh Token을 이용해 Access Token을 갱신할 수 있으나, 서버에서 검증이 필요
Refresh Token 저장 방식 및 보안 고려 사항
Refresh Token은 사용자의 인증 정보를 장기간 유지하는 역할을 하기 때문에,
어디에 저장하고 어떻게 관리할지 신중한 접근이 필요하다.
아래는 보안적으로 권장되는 Refresh Token 저장 방식과 그에 따른 고려 사항이다.

HTTP-Only Secure Cookie 저장 방식
XSS 공격을 방어할 수 있도록 JavaScript에서 접근 불가능한 HttpOnly 속성을 추가.
Secure 속성을 설정하여 HTTPS 환경에서만 전송되도록 제한.
SameSite 옵션을 이용해 CSRF 공격을 방어.
ResponseCookie refreshTokenCookie = ResponseCookie.from("refresh_token", refreshToken)
        .httpOnly(true)
        .secure(true)
        .sameSite("Strict")
        .path("/")
        .maxAge(Duration.ofDays(30))  // 30일 동안 유지
        .build();
response.addHeader("Set-Cookie", refreshTokenCookie.toString());
데이터베이스 또는 Redis에 저장
Refresh Token을 클라이언트가 직접 관리하는 대신 서버에서 안전하게 관리.
로그인할 때마다 새로운 Refresh Token을 발급하고 기존 Token을 폐기하는 방식 적용.
빠른 조회를 위해 Redis를 사용하여 Token 상태 관리.
public void storeRefreshToken(String userId, String refreshToken) {
    redisTemplate.opsForValue().set("refresh_token:" + userId, refreshToken, 30, TimeUnit.DAYS);
}

public boolean validateRefreshToken(String userId, String refreshToken) {
    String storedToken = redisTemplate.opsForValue().get("refresh_token:" + userId);
    return storedToken != null && storedToken.equals(refreshToken);
}
디바이스 바인딩(Device Binding)
Refresh Token을 단순히 저장하는 것이 아니라, 사용자의 특정 디바이스와 연결하여 사용.
디바이스 변경 시 Refresh Token을 재발급하도록 설정.
Refresh Token을 활용한 보안 강화 전략
Refresh Token은 장기적으로 보관되는 토큰이므로, 보안을 강화할 필요가 있다.
다음과 같은 전략을 적용하면 Refresh Token을 보다 안전하게 관리할 수 있다.

Refresh Token의 유효 기간 제한
Refresh Token을 무기한 사용하면 보안 위협이 커질 수 있다.
보통 7일~30일 정도의 유효 기간을 설정하고, 주기적으로 갱신해야 한다.
String refreshToken = Jwts.builder()
        .setSubject("user123")
        .setIssuedAt(new Date())
        .setExpiration(new Date(System.currentTimeMillis() + TimeUnit.DAYS.toMillis(30))) // 30일 후 만료
        .signWith(SignatureAlgorithm.HS256, secretKey)
        .compact();
Refresh Token을 사용한 Access Token 재발급 정책
Refresh Token을 검증할 때 동일한 Refresh Token을 다시 사용하지 않도록 처리.
매번 새로운 Refresh Token을 발급하고, 기존 Token은 폐기.
public String refreshAccessToken(String refreshToken) {
    if (validateRefreshToken(refreshToken)) {
        String newAccessToken = generateAccessToken();
        String newRefreshToken = generateRefreshToken();
        storeRefreshToken("user123", newRefreshToken); // 기존 Token을 갱신
        return newAccessToken;
    }
    throw new InvalidTokenException("Invalid Refresh Token");
}
Refresh Token 탈취 대응 (ROTATE REFRESH TOKEN)
Refresh Token이 유출될 경우를 대비하여 "Refresh Token Rotation" 정책을 적용.
클라이언트가 Refresh Token을 사용할 때마다 새로운 Refresh Token을 발급.
기존 Token은 즉시 폐기하고, 유효하지 않도록 설정.
public String rotateRefreshToken(String userId, String oldRefreshToken) {
    String storedToken = redisTemplate.opsForValue().get("refresh_token:" + userId);
    if (storedToken == null || !storedToken.equals(oldRefreshToken)) {
        throw new InvalidTokenException("Invalid or Expired Refresh Token");
    }

    // 새 Refresh Token 발급 및 저장
    String newRefreshToken = generateRefreshToken();
    storeRefreshToken(userId, newRefreshToken);
    return newRefreshToken;
}
Refresh Token 재사용 공격 방지
Refresh Token을 여러 번 사용할 수 없도록 제한.
Refresh Token이 한 번 사용되면, 즉시 폐기.
public void revokeRefreshToken(String userId) {
    redisTemplate.delete("refresh_token:" + userId);  // Refresh Token 삭제
}
IP 및 기기 정보 기반 검증
Refresh Token 요청 시, 클라이언트의 IP 주소 및 User-Agent 정보를 확인.
이전에 로그인한 환경과 다른 경우 추가 인증을 요구.
public boolean isSuspiciousRequest(String userId, String clientIp, String userAgent) {
    String storedIp = redisTemplate.opsForValue().get("ip:" + userId);
    String storedUserAgent = redisTemplate.opsForValue().get("ua:" + userId);

    return !storedIp.equals(clientIp) || !storedUserAgent.equals(userAgent);
}
Refresh Token 기반 인증 흐름
사용자가 로그인하면 Access Token과 Refresh Token을 발급.
Access Token이 만료되면, Refresh Token을 이용해 새로운 Access Token을 요청.
Refresh Token이 유효하면 새로운 Access Token과 Refresh Token을 발급.
기존 Refresh Token을 폐기하고 새로운 Token으로 교체.
Refresh Token 적용 방식 요약
보안 기법	설명	적용 방법
HTTP-Only Secure Cookie	클라이언트에서 직접 접근 불가	HttpOnly, Secure, SameSite 설정
데이터베이스 저장	서버에서 Refresh Token 관리	Redis 또는 DB 활용
Device Binding	특정 디바이스와 Refresh Token을 연결	기기 ID와 함께 저장
Refresh Token Rotation	사용될 때마다 새로운 Token 발급	기존 Token 즉시 폐기
IP 및 User-Agent 검증	이전 로그인 환경과 비교	Redis에 IP/User-Agent 저장 후 비교
학습자의 사고를 돕기 위한 질문
Refresh Token을 클라이언트 측에 저장하는 방식과 서버 측에서 관리하는 방식의 차이점은 무엇인가?

보안성과 편의성의 균형을 고려해보라.
Refresh Token이 탈취될 경우 발생할 수 있는 보안 문제를 방지하기 위한 방안에는 어떤 것이 있는가?

Refresh Token Rotation, IP 제한 등의 전략을 생각해보라.
7.4. OAuth2와 JWT 기반의 권한(Role) 관리
OAuth2와 JWT 기반의 인증 시스템을 구축할 때, 권한(Role) 관리는 필수적인 요소이다.
API가 보호되어야 할 리소스에 접근할 수 있는 사용자를 구분하고,
각 사용자가 수행할 수 있는 액션을 명확히 정의해야 한다.

JWT를 사용하면 사용자의 권한 정보를 포함하여 토큰을 발급할 수 있으며,
이 권한 정보를 기반으로 API에 대한 접근을 제어할 수 있다.
Spring Security를 활용하면, RBAC(Role-Based Access Control) 또는 Scope 기반 권한 관리를 적용할 수 있다.

JWT 기반의 Role (권한) 관리 방식
JWT를 활용한 권한 관리는 크게 두 가지 방법으로 나눌 수 있다.

Role-Based Access Control (RBAC)

사용자의 역할(Role)에 따라 접근을 제어하는 방식.
예: ADMIN, USER, MANAGER 등 역할을 기반으로 API 접근 권한을 부여.
Scope-Based Access Control

OAuth2의 Scope를 활용하여 권한을 제어.
예: read, write, delete 등의 특정 기능에 대한 권한을 부여.
JWT에 Role 정보 포함하기
JWT의 Payload(페이로드)에는 사용자의 Role 또는 Scope 정보를 포함할 수 있다.

{
  "sub": "user123",
  "roles": ["ROLE_USER", "ROLE_ADMIN"],
  "exp": 1710508800
}
위 JSON 구조에서 "roles" 필드는 사용자의 역할 정보를 포함하며,
이를 기반으로 API 접근을 제어할 수 있다.

Spring Security에서 JWT 기반 Role 관리 적용
Spring Security에서는 JWT에 포함된 Role 정보를 활용하여 API 접근을 제어할 수 있다.
이를 위해 @PreAuthorize, @PostAuthorize 또는 SecurityFilterChain을 설정할 수 있다.

JWT에서 Role 정보를 추출하는 필터 구현
JWT의 Payload에서 Role 정보를 가져와 Spring Security의 Authentication 객체에 저장.
@Component
public class JwtAuthorizationFilter extends OncePerRequestFilter {

    private final JwtUtil jwtUtil;

    public JwtAuthorizationFilter(JwtUtil jwtUtil) {
        this.jwtUtil = jwtUtil;
    }

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain chain)
            throws ServletException, IOException {
        
        String token = jwtUtil.resolveToken(request);
        if (token != null && jwtUtil.validateToken(token)) {
            Claims claims = jwtUtil.getClaims(token);
            String username = claims.getSubject();
            List<GrantedAuthority> authorities = jwtUtil.getRolesFromToken(claims);
            
            Authentication auth = new UsernamePasswordAuthenticationToken(username, null, authorities);
            SecurityContextHolder.getContext().setAuthentication(auth);
        }
        chain.doFilter(request, response);
    }
}
JWT 유틸리티 클래스에서 Role 추출 로직
JWT에서 Role 정보를 가져와 GrantedAuthority 리스트로 변환.
@Component
public class JwtUtil {

    private final String secretKey = "mySecretKey";

    public Claims getClaims(String token) {
        return Jwts.parser()
                .setSigningKey(secretKey)
                .parseClaimsJws(token)
                .getBody();
    }

    public List<GrantedAuthority> getRolesFromToken(Claims claims) {
        List<String> roles = claims.get("roles", List.class);
        return roles.stream().map(SimpleGrantedAuthority::new).collect(Collectors.toList());
    }
}
Spring Security에서 Role을 기반으로 접근 제어 설정
JWT를 통해 Role 정보를 Spring Security에 전달하면,
이를 활용해 API 접근 권한을 제어할 수 있다.

컨트롤러 단에서 @PreAuthorize를 사용한 Role 기반 접근 제어
특정 Role을 가진 사용자만 API를 호출할 수 있도록 설정.
@RestController
@RequestMapping("/admin")
public class AdminController {

    @GetMapping("/dashboard")
    @PreAuthorize("hasRole('ADMIN')")
    public ResponseEntity<String> getAdminDashboard() {
        return ResponseEntity.ok("관리자 대시보드");
    }
}
SecurityFilterChain을 사용하여 Role 기반 접근 제어
/admin/** 경로는 ADMIN Role을 가진 사용자만 접근 가능하도록 설정.
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    return http
        .authorizeHttpRequests(auth -> auth
            .requestMatchers("/admin/**").hasRole("ADMIN")
            .requestMatchers("/user/**").hasAnyRole("USER", "ADMIN")
            .anyRequest().authenticated()
        )
        .sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
        .addFilterBefore(new JwtAuthorizationFilter(jwtUtil), UsernamePasswordAuthenticationFilter.class)
        .build();
}
Scope 기반의 권한 관리
OAuth2를 사용할 때 Scope를 활용하여 세부적인 권한을 제어할 수 있다.

JWT에 Scope 정보 포함하기
scope 필드를 추가하여 특정 기능에 대한 권한을 지정.
{
  "sub": "user123",
  "scope": ["read", "write"]
}
Scope 기반 접근 제어 적용
특정 Scope를 가진 사용자만 API를 호출하도록 설정.
@PreAuthorize("hasAuthority('SCOPE_read')")
@GetMapping("/data")
public ResponseEntity<String> getData() {
    return ResponseEntity.ok("데이터 접근 성공");
}
SecurityFilterChain에서 Scope를 기반으로 접근 제어
SCOPE_read 또는 SCOPE_write 권한을 기반으로 API 접근을 제한.
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    return http
        .authorizeHttpRequests(auth -> auth
            .requestMatchers("/api/read").hasAuthority("SCOPE_read")
            .requestMatchers("/api/write").hasAuthority("SCOPE_write")
            .anyRequest().authenticated()
        )
        .sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
        .build();
}
OAuth2와 JWT 기반 권한 관리 전략
권한 관리 방식	설명	적용 방식
Role-Based Access Control (RBAC)	사용자의 역할(Role)에 따라 접근 권한을 부여	@PreAuthorize("hasRole('ADMIN')")
Scope-Based Access Control	OAuth2의 Scope를 기반으로 권한을 관리	@PreAuthorize("hasAuthority('SCOPE_read')")
JWT에 Scope 정보 포함	JWT의 Payload에 Scope 정보 저장	{ "scope": ["read", "write"] }
SecurityFilterChain 설정	특정 Role/Scope만 API 접근 가능하도록 설정	.requestMatchers("/admin/**").hasRole("ADMIN")
실습 문제
문제 1: JWT 기반의 역할(Role) 부여 및 검증
아래 요구사항을 만족하는 코드를 작성하시오.

JWT의 Payload에 사용자의 역할(Role)을 추가한다.
ROLE_USER, ROLE_ADMIN 두 가지 역할을 가진 사용자를 설정한다.
ROLE_ADMIN만 접근 가능한 API를 구현하고, ROLE_USER가 접근할 경우 거부 메시지를 반환하도록 한다.
문제 2: Spring Security에서 OAuth2 권한(Role) 검증
다음 요구사항을 만족하는 코드를 작성하시오.

OAuth2 기반 로그인 시, 사용자 정보를 가져와 Spring Security에서 권한을 설정한다.
특정 API에 @PreAuthorize("hasRole('ADMIN')")를 적용하여 ADMIN 권한을 가진 사용자만 접근 가능하도록 한다.
USER 권한을 가진 사용자가 접근 시 403 Forbidden 응답을 반환해야 한다.
연습 문제
문제 1: JWT의 구조 분석
JWT를 분석하는 프로그램을 작성하시오.

JWT는 Header.Payload.Signature로 구성된다. 예제 토큰(eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...)을 분석하여 Header와 Payload를 추출하시오.
Header와 Payload는 Base64로 인코딩되어 있다. Base64 디코딩을 사용하여 Header와 Payload를 JSON 형식으로 변환하시오.
Payload에서 exp(토큰 만료 시간) 값을 확인하고, 현재 시간과 비교하여 토큰이 만료되었는지 판단하는 기능을 추가하시오.
문제 2: JWT 생성 및 서명
다음 요구사항을 만족하는 JWT 발급 프로그램을 작성하시오.

사용자의 id, role, exp(만료 시간)를 포함하는 JWT를 생성하시오.
HMAC SHA256 알고리즘을 사용하여 JWT를 서명(Signature)하시오.
생성된 JWT를 출력하시오.
문제 3: OAuth2 기반의 JWT 발급
OAuth2 인증 서버를 구현하여 JWT 기반 Access Token을 발급하는 프로그램을 작성하시오.

OAuth2 인증 서버를 구성하고, 클라이언트가 로그인을 요청하면 JWT를 발급하도록 설정하시오.
인증이 성공하면 발급된 JWT를 클라이언트에게 반환하도록 구현하시오.
인증 요청 시 클라이언트 ID와 비밀번호를 검증하는 로직을 추가하시오.
문제 4: OAuth2 Access Token 검증
OAuth2 기반의 JWT 인증을 검증하는 프로그램을 작성하시오.

클라이언트가 OAuth2 인증 서버에서 발급받은 JWT를 리소스 서버에 전송하도록 설정하시오.
리소스 서버에서 Authorization 헤더의 JWT를 검증하는 로직을 추가하시오.
JWT가 유효하면 요청을 정상적으로 처리하고, 유효하지 않으면 401 Unauthorized 응답을 반환하도록 구현하시오.
문제 5: JWT를 활용한 사용자 인증
JWT 기반 사용자 인증 시스템을 구현하시오.

사용자가 로그인하면 JWT를 생성하여 클라이언트에 반환하도록 구현하시오.
클라이언트가 API 요청을 보낼 때 JWT를 포함하도록 설정하시오.
서버는 JWT를 검증하고, 유효한 경우 사용자 정보를 반환하도록 구현하시오.
문제 6: Refresh Token을 이용한 Access Token 갱신
Refresh Token을 이용하여 Access Token을 갱신하는 기능을 구현하시오.

사용자가 로그인하면 Access Token과 Refresh Token을 함께 발급하도록 설정하시오.
클라이언트가 Access Token이 만료되었을 때 Refresh Token을 사용하여 새로운 Access Token을 요청할 수 있도록 구현하시오.
Refresh Token이 유효한 경우 새로운 Access Token을 발급하고, 그렇지 않으면 401 Unauthorized를 반환하도록 설정하시오.
문제 7: JWT 기반의 Spring Security 인증
Spring Security를 활용하여 JWT 인증 필터를 구현하시오.

Spring Security의 OncePerRequestFilter를 확장하여 JWT 인증 필터를 생성하시오.
HTTP 요청의 Authorization 헤더에서 JWT를 추출하고 검증하는 로직을 추가하시오.
JWT가 유효한 경우 SecurityContext에 사용자 정보를 저장하도록 설정하시오.
문제 8: OAuth2 SSO 기반 로그인 구현
OAuth2 기반의 Single Sign-On(SSO) 인증을 구현하시오.

OAuth2 인증 서버를 구현하여 사용자가 로그인하면 Access Token을 발급하도록 설정하시오.
클라이언트가 발급된 Access Token을 사용하여 리소스 서버에 접근할 수 있도록 구현하시오.
로그인된 사용자가 다른 애플리케이션에서도 동일한 인증 상태를 유지할 수 있도록 설정하시오.
문제 9: JWT 기반 권한(Role) 검증
JWT 기반의 역할(Role) 관리 기능을 구현하시오.

JWT의 Payload에 사용자의 역할(ROLE_USER, ROLE_ADMIN)을 추가하시오.
특정 API 엔드포인트가 ROLE_ADMIN만 접근 가능하도록 구현하시오.
ROLE_USER가 ROLE_ADMIN 전용 API에 접근할 경우 403 Forbidden 응답을 반환하도록 설정하시오.
문제 10: OAuth2 인증 서버에서 클라이언트 인증 처리
OAuth2 인증 서버에서 클라이언트 인증을 처리하는 기능을 구현하시오.

OAuth2 인증 서버에서 클라이언트 ID와 클라이언트 비밀번호를 기반으로 인증을 수행하도록 설정하시오.
인증이 성공하면 Access Token을 발급하여 반환하시오.
클라이언트가 잘못된 자격 증명을 입력하면 401 Unauthorized 응답을 반환하도록 구현하시오.
답안
1. OAuth2 개요
1.1. OAuth2의 개념
1.1.1 질문에 대한 답안
OAuth2는 기존의 인증 방식과 비교했을 때 어떤 차이점이 있는가?

기존의 인증 방식은 사용자 자격 증명을 직접 서버에 전달하여 인증하는 방식이지만, OAuth2는 토큰 기반의 인증 방식을 사용하여 사용자의 인증 정보를 직접 공유하지 않고 접근 권한을 부여한다.
OAuth2에서 '토큰'을 활용하는 이유는 무엇인가?

토큰을 활용하면 사용자의 실제 인증 정보(아이디, 비밀번호 등)를 직접 전달하지 않고도 보안성을 유지할 수 있다. 또한, 세션 관리가 필요 없으며, 다양한 클라이언트(웹, 모바일)에서 인증을 쉽게 처리할 수 있다.
1.2. OAuth2의 인증 방식
1.2.1 질문에 대한 답안
Authorization Code Grant 방식이 보안적으로 가장 안전한 이유는 무엇인가?

Access Token이 클라이언트에 직접 노출되지 않으며, 인증 코드가 서버를 통해 교환되므로 MITM(중간자 공격) 등의 보안 위협을 줄일 수 있다.
Implicit Grant 방식이 점점 사용되지 않는 이유는 무엇인가?

Access Token이 클라이언트 측(JavaScript)에서 직접 처리되기 때문에 토큰이 쉽게 탈취될 위험이 있다. 따라서 보안성이 떨어지며, 점차 사용이 줄어들고 있다.
1.3. OAuth2와 OpenID Connect (OIDC)
1.3.1 질문에 대한 답안
OAuth2는 인증(Authentication) 프로토콜이 아닌 이유는 무엇인가?

OAuth2는 사용자의 권한을 제3자에게 위임하는 프로토콜이며, 사용자의 인증을 보장하지 않는다. 즉, OAuth2 자체는 사용자가 누구인지 인증하는 기능을 제공하지 않는다.
OpenID Connect(OIDC)가 OAuth2와 함께 사용될 때 제공하는 추가적인 기능은 무엇인가?

OpenID Connect(OIDC)는 ID Token을 제공하여 사용자의 신원 정보를 포함하는 기능을 제공한다. 이를 통해 OAuth2의 한계를 보완하고, 사용자의 인증을 보장할 수 있다.
2. JWT(Json Web Token) 개요
2.1. JWT의 개념
2.1.1 질문에 대한 답안
JWT는 왜 JSON 형식을 사용하여 정보를 저장하는가?

JSON은 가볍고, 구조화된 데이터를 쉽게 표현할 수 있으며, 다양한 프로그래밍 언어에서 지원되기 때문에 데이터 교환에 용이하다.
JWT가 일반적인 세션 기반 인증 방식과 비교했을 때 가지는 장점은 무엇인가?

JWT는 서버에서 세션을 유지할 필요 없이(stateless) , 각 요청에서 자체적으로 사용자 정보를 포함할 수 있어 분산 시스템이나 마이크로서비스 환경에서 효율적이다.
2.2. JWT의 동작 방식
2.2.1 질문에 대한 답안
JWT가 서버에서 사용자의 인증 정보를 검증할 때 데이터베이스 조회 없이도 검증할 수 있는 이유는 무엇인가?

JWT에는 사용자의 인증 정보와 서명이 포함되어 있으므로, 서명을 검증하는 것만으로 해당 토큰이 유효한지 확인할 수 있다.
JWT가 클라이언트-서버 간의 인증 과정에서 일반적인 쿠키-세션 방식보다 효율적인 경우는 언제인가?

분산 시스템이나 마이크로서비스 환경에서는 중앙에서 세션을 관리하는 것이 어렵기 때문에, JWT를 사용하면 각 서비스가 독립적으로 사용자 인증을 처리할 수 있다.
2.2.2 실습 문제에 대한 답안
문제 1: JWT의 구조 분석

import java.util.Base64;

public class JWTDecoder {
    public static void main(String[] args) {
        String jwt = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJ1c2VyMTIzIiwiZXhwIjoxNjk3MDE5MjAwLCJpYXQiOjE2OTcwMTU2MDB9.abc123signature";

        String[] parts = jwt.split("\\.");
        System.out.println("Header: " + new String(Base64.getUrlDecoder().decode(parts[0])));
        System.out.println("Payload: " + new String(Base64.getUrlDecoder().decode(parts[1])));
    }
}
문제 2: JWT 발급과 검증 흐름 이해

import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import io.jsonwebtoken.Claims;

import java.util.Date;
import java.util.Base64;

public class JWTExample {
    private static final String SECRET_KEY = "mySecretKey";

    public static void main(String[] args) {
        String token = generateToken("user123", "ROLE_USER");
        System.out.println("Generated Token: " + token);

        Claims claims = validateToken(token);
        System.out.println("User ID: " + claims.getSubject());
        System.out.println("User Role: " + claims.get("role"));
    }

    public static String generateToken(String userId, String role) {
        return Jwts.builder()
                .setSubject(userId)
                .claim("role", role)
                .setIssuedAt(new Date())
                .setExpiration(new Date(System.currentTimeMillis() + 1000 * 60 * 60)) // 1시간 유효
                .signWith(SignatureAlgorithm.HS256, Base64.getEncoder().encodeToString(SECRET_KEY.getBytes()))
                .compact();
    }

    public static Claims validateToken(String token) {
        return Jwts.parser()
                .setSigningKey(Base64.getEncoder().encodeToString(SECRET_KEY.getBytes()))
                .parseClaimsJws(token)
                .getBody();
    }
}
2.3. JWT의 장점과 보안 고려 사항
2.3.1 질문에 대한 답안
JWT의 stateless 특성이 인증 시스템에서 어떤 이점을 제공하는가?

서버에서 세션을 유지할 필요가 없으므로, 확장성 있는 아키텍처(예: 마이크로서비스, 로드 밸런싱)에서 유용하다.
JWT를 사용할 때 보안적으로 고려해야 할 주요 사항은 무엇인가?

토큰 탈취 방지(HTTPS 사용) , 짧은 유효 기간 설정, 서명 검증 강화 등이 필요하다.
3. OAuth2와 JWT의 관계 및 통합 개념
3.1. OAuth2에서 JWT를 사용하는 이유
3.1.1 질문에 대한 답안
OAuth2는 원래 자체적인 인증 방식(예: Authorization Code Grant)을 제공하는데, 왜 JWT를 사용하여 인증을 보완하는가?

OAuth2는 클라이언트가 서버에서 Access Token을 발급받아 사용하는 방식이지만, 이 Access Token이 데이터베이스에 저장되면 서버의 부담이 커진다.
JWT를 사용하면 토큰 자체에 인증 정보를 포함하여 검증할 수 있어, 데이터베이스 조회 없이 인증할 수 있다는 장점이 있다.
JWT를 OAuth2의 Access Token으로 활용할 경우, 기존의 OAuth2 토큰 방식과 비교했을 때 어떤 장점이 있는가?

기존의 OAuth2 토큰은 서버에서 저장 및 검증해야 하지만, JWT는 서버에서 검증만 수행하고 추가적인 데이터베이스 조회 없이 처리할 수 있다.
또한 JWT는 서명이 포함되어 있어 위변조가 불가능하며, 만료 시간을 직접 지정할 수 있다.
3.2. OAuth2 기반 JWT 인증 흐름
3.2.1 질문에 대한 답안
OAuth2 기반 시스템에서 Access Token이 발급될 때, JWT를 사용하면 서버의 부하를 줄일 수 있는 이유는 무엇인가?

기존의 Access Token은 서버에서 저장하고 검증해야 하지만, JWT는 토큰 자체에 사용자 정보를 포함하므로 데이터베이스 조회 없이 검증 가능하다.
이를 통해 서버의 부하를 줄이고 고성능 API 인증 시스템을 구현할 수 있다.
JWT 기반의 OAuth2 인증이 적용될 경우, 사용자의 요청이 처리되는 과정에서 서버가 JWT를 검증하는 단계는 무엇인가?

클라이언트가 API 요청 시 Authorization 헤더에 JWT를 포함하여 전송한다.
서버는 JWT의 서명을 검증하고, 유효한 경우 요청을 처리하며, 유효하지 않은 경우 인증 실패 응답(401 Unauthorized)을 반환한다.
3.2.2 실습 문제에 대한 답안
문제 1: OAuth2 인증 서버에서 JWT 발급 흐름 이해

@Configuration
@EnableAuthorizationServer
public class OAuth2AuthorizationServerConfig extends AuthorizationServerConfigurerAdapter {

    @Autowired
    private AuthenticationManager authenticationManager;

    @Override
    public void configure(ClientDetailsServiceConfigurer clients) throws Exception {
        clients.inMemory()
                .withClient("clientId")
                .secret("{noop}clientSecret")
                .authorizedGrantTypes("password", "refresh_token")
                .scopes("read", "write")
                .accessTokenValiditySeconds(3600)
                .refreshTokenValiditySeconds(7200);
    }

    @Override
    public void configure(AuthorizationServerEndpointsConfigurer endpoints) {
        endpoints.authenticationManager(authenticationManager)
                .accessTokenConverter(jwtAccessTokenConverter());
    }

    @Bean
    public JwtAccessTokenConverter jwtAccessTokenConverter() {
        JwtAccessTokenConverter converter = new JwtAccessTokenConverter();
        converter.setSigningKey("secretKey"); // 서명 키
        return converter;
    }
}
문제 2: JWT를 사용한 OAuth2 인증 검증 프로세스

@Configuration
@EnableResourceServer
public class OAuth2ResourceServerConfig extends ResourceServerConfigurerAdapter {

    @Override
    public void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
                .antMatchers("/public").permitAll()
                .antMatchers("/secure").authenticated();
    }

    @Override
    public void configure(ResourceServerSecurityConfigurer resources) {
        resources.tokenStore(tokenStore());
    }

    @Bean
    public TokenStore tokenStore() {
        return new JwtTokenStore(jwtAccessTokenConverter());
    }

    @Bean
    public JwtAccessTokenConverter jwtAccessTokenConverter() {
        JwtAccessTokenConverter converter = new JwtAccessTokenConverter();
        converter.setSigningKey("secretKey"); // 서명 키
        return converter;
    }
}
3.3. Access Token과 Refresh Token의 차이
3.3.1 질문에 대한 답안
Access Token과 Refresh Token은 각각 언제 사용되며, Refresh Token이 필요한 이유는 무엇인가?

Access Token은 짧은 시간 동안 유효하며, 클라이언트가 API 요청을 보낼 때 사용된다.
Refresh Token은 Access Token이 만료되었을 때 새로운 Access Token을 발급받기 위해 사용되며, 사용자의 재인증 과정을 최소화할 수 있다.
Refresh Token이 Access Token보다 보안 측면에서 더 강력하게 보호되어야 하는 이유는 무엇인가?

Refresh Token이 탈취되면 새로운 Access Token을 계속 생성할 수 있기 때문에 보안적으로 큰 위협이 된다.
따라서 Refresh Token은 데이터베이스 또는 보안성이 강화된 저장소(예: Redis)에 저장하고, 클라이언트가 직접 접근할 수 없도록 해야 한다.
4. Spring Security에서 OAuth2 및 JWT 통합
4.1. OAuth2 인증 구현
4.1.1 실습 문제에 대한 답안
문제 1: OAuth2 인증 서버 설정

@Configuration
@EnableAuthorizationServer
public class OAuth2AuthServerConfig extends AuthorizationServerConfigurerAdapter {

    @Autowired
    private AuthenticationManager authenticationManager;

    @Override
    public void configure(ClientDetailsServiceConfigurer clients) throws Exception {
        clients.inMemory()
                .withClient("myClient")
                .secret("{noop}secret")
                .authorizedGrantTypes("authorization_code", "refresh_token")
                .scopes("read");
    }

    @Override
    public void configure(AuthorizationServerEndpointsConfigurer endpoints) {
        endpoints.authenticationManager(authenticationManager)
                .accessTokenConverter(accessTokenConverter());
    }

    @Bean
    public JwtAccessTokenConverter accessTokenConverter() {
        JwtAccessTokenConverter converter = new JwtAccessTokenConverter();
        converter.setSigningKey("mySecretKey");
        return converter;
    }
}
문제 2: OAuth2 클라이언트 설정

@Configuration
@EnableOAuth2Client
public class OAuth2ClientConfig {

    @Bean
    public OAuth2RestTemplate oauth2RestTemplate(OAuth2ClientContext oauth2ClientContext) {
        OAuth2RestTemplate template = new OAuth2RestTemplate(resourceDetails(), oauth2ClientContext);
        return template;
    }

    @Bean
    public AuthorizationCodeResourceDetails resourceDetails() {
        AuthorizationCodeResourceDetails details = new AuthorizationCodeResourceDetails();
        details.setClientId("myClient");
        details.setClientSecret("secret");
        details.setAccessTokenUri("http://localhost:8080/oauth/token");
        details.setUserAuthorizationUri("http://localhost:8080/oauth/authorize");
        details.setScope(List.of("read"));
        return details;
    }
}
4.2. Spring Security에서 JWT 적용
4.2.1 실습 문제에 대한 답안
문제 1: JWT를 사용한 인증 필터 구현

@Component
public class JwtAuthenticationFilter extends OncePerRequestFilter {

    @Autowired
    private JwtTokenProvider jwtTokenProvider;

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain chain)
            throws ServletException, IOException {
        String token = jwtTokenProvider.resolveToken(request);
        if (token != null && jwtTokenProvider.validateToken(token)) {
            Authentication auth = jwtTokenProvider.getAuthentication(token);
            SecurityContextHolder.getContext().setAuthentication(auth);
        }
        chain.doFilter(request, response);
    }
}
문제 2: JWT 기반 로그인 구현

@RestController
@RequestMapping("/auth")
public class AuthController {

    @Autowired
    private AuthenticationManager authenticationManager;

    @Autowired
    private JwtTokenProvider jwtTokenProvider;

    @PostMapping("/login")
    public ResponseEntity<?> login(@RequestBody AuthRequest request) {
        Authentication authentication = authenticationManager.authenticate(
                new UsernamePasswordAuthenticationToken(request.getUsername(), request.getPassword()));
        String token = jwtTokenProvider.createToken(request.getUsername(), authentication.getAuthorities());
        return ResponseEntity.ok(new AuthResponse(token));
    }
}

class AuthRequest {
    private String username;
    private String password;
    // Getters and Setters
}

class AuthResponse {
    private String token;
    public AuthResponse(String token) { this.token = token; }
    // Getter
}
4.3. OAuth2 및 JWT 설정을 위한 주요 컴포넌트
4.3.1 실습 문제에 대한 답안
문제 1: JwtDecoder와 JwtEncoder를 사용한 JWT 발급 및 검증

@Configuration
public class JwtConfig {

    @Value("${jwt.secret}")
    private String secretKey;

    @Bean
    public JwtEncoder jwtEncoder() {
        return new NimbusJwtEncoder(new ImmutableSecret<>(secretKey.getBytes()));
    }

    @Bean
    public JwtDecoder jwtDecoder() {
        return NimbusJwtDecoder.withSecretKey(secretKey.getBytes()).build();
    }
}
문제 2: AuthenticationManager와 SecurityContextHolder를 활용한 사용자 인증

@Service
public class JwtTokenProvider {

    @Value("${jwt.secret}")
    private String secretKey;

    @Autowired
    private UserDetailsService userDetailsService;

    public String createToken(String username, Collection<? extends GrantedAuthority> roles) {
        Claims claims = Jwts.claims().setSubject(username);
        claims.put("roles", roles.stream().map(GrantedAuthority::getAuthority).collect(Collectors.toList()));

        Date now = new Date();
        Date expiry = new Date(now.getTime() + 3600000);

        return Jwts.builder()
                .setClaims(claims)
                .setIssuedAt(now)
                .setExpiration(expiry)
                .signWith(SignatureAlgorithm.HS256, secretKey)
                .compact();
    }

    public Authentication getAuthentication(String token) {
        UserDetails userDetails = userDetailsService.loadUserByUsername(getUsername(token));
        return new UsernamePasswordAuthenticationToken(userDetails, "", userDetails.getAuthorities());
    }

    public String getUsername(String token) {
        return Jwts.parser().setSigningKey(secretKey).parseClaimsJws(token).getBody().getSubject();
    }
}
5. JWT 발급 및 검증 구현
5.1. JWT 생성 및 서명
5.1.1 실습 문제에 대한 답안
문제 1: HMAC 기반의 JWT 생성

public class JwtUtil {

    private static final String SECRET_KEY = "mySecretKey";

    public static String generateToken(String username) {
        return Jwts.builder()
                .setSubject(username)
                .setIssuedAt(new Date())
                .setExpiration(new Date(System.currentTimeMillis() + 3600000))
                .signWith(SignatureAlgorithm.HS256, SECRET_KEY)
                .compact();
    }
}
문제 2: RSA 기반의 JWT 서명

public class RsaJwtUtil {

    private static KeyPair keyPair = generateKeyPair();

    private static KeyPair generateKeyPair() {
        try {
            KeyPairGenerator keyGen = KeyPairGenerator.getInstance("RSA");
            keyGen.initialize(2048);
            return keyGen.generateKeyPair();
        } catch (Exception e) {
            throw new RuntimeException("KeyPair 생성 실패", e);
        }
    }

    public static String generateToken(String username) {
        return Jwts.builder()
                .setSubject(username)
                .setIssuedAt(new Date())
                .setExpiration(new Date(System.currentTimeMillis() + 3600000))
                .signWith(SignatureAlgorithm.RS256, keyPair.getPrivate())
                .compact();
    }

    public static boolean validateToken(String token) {
        try {
            Jws<Claims> claims = Jwts.parser().setSigningKey(keyPair.getPublic()).parseClaimsJws(token);
            return !claims.getBody().getExpiration().before(new Date());
        } catch (Exception e) {
            return false;
        }
    }
}
5.2. JWT 검증 및 인증 처리
5.2.1 실습 문제에 대한 답안
문제 1: JWT를 검증하는 필터 구현

@Component
public class JwtVerificationFilter extends OncePerRequestFilter {

    @Autowired
    private JwtTokenProvider jwtTokenProvider;

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain chain)
            throws ServletException, IOException {
        String token = jwtTokenProvider.resolveToken(request);
        if (token != null && jwtTokenProvider.validateToken(token)) {
            Authentication auth = jwtTokenProvider.getAuthentication(token);
            SecurityContextHolder.getContext().setAuthentication(auth);
        }
        chain.doFilter(request, response);
    }
}
문제 2: JWT를 활용한 사용자 인증 API 구현

@RestController
@RequestMapping("/user")
public class UserController {

    @GetMapping("/info")
    public ResponseEntity<?> getUserInfo(Authentication authentication) {
        return ResponseEntity.ok().body(authentication.getPrincipal());
    }
}
5.3. Refresh Token을 활용한 Access Token 갱신
5.3.1 실습 문제에 대한 답안
문제 1: Refresh Token을 활용한 JWT 갱신

@RestController
@RequestMapping("/auth")
public class RefreshTokenController {

    @Autowired
    private JwtTokenProvider jwtTokenProvider;

    @PostMapping("/refresh")
    public ResponseEntity<?> refresh(@RequestBody RefreshTokenRequest request) {
        if (jwtTokenProvider.validateToken(request.getRefreshToken())) {
            String newAccessToken = jwtTokenProvider.createToken(jwtTokenProvider.getUsername(request.getRefreshToken()), Collections.emptyList());
            return ResponseEntity.ok(new AuthResponse(newAccessToken));
        }
        return ResponseEntity.status(HttpStatus.UNAUTHORIZED).build();
    }
}
문제 2: Refresh Token 저장 및 보안 처리

@Service
public class RefreshTokenService {

    private Map<String, String> refreshTokenStore = new ConcurrentHashMap<>();

    public void storeToken(String username, String refreshToken) {
        refreshTokenStore.put(username, refreshToken);
    }

    public boolean validateRefreshToken(String username, String refreshToken) {
        return refreshToken.equals(refreshTokenStore.get(username));
    }

    public void removeToken(String username) {
        refreshTokenStore.remove(username);
    }
}
6. OAuth2 + JWT를 활용한 SSO 구현
6.1. SSO(Single Sign-On) 개요
6.1.1 학습자의 사고를 돕기 위한 질문
SSO(Single Sign-On)는 왜 필요하며, 어떤 환경에서 가장 유용하게 사용될 수 있는가?

기업 환경이나 여러 서비스가 존재하는 플랫폼에서 사용자 경험을 고려해보라.
OAuth2와 JWT를 활용하여 SSO를 구현할 때, 각 기술이 담당하는 역할은 무엇인가?

OAuth2가 인증 과정을 관리하는 방식과 JWT가 사용자 정보를 저장하는 방식을 비교해보라.
6.2. OAuth2 기반의 SSO 구현
6.2.1 실습 문제에 대한 답안
문제 1: OAuth2 기반의 SSO 로그인 구현

@RestController
@RequestMapping("/sso")
public class SsoController {

    @Autowired
    private JwtTokenProvider jwtTokenProvider;

    @PostMapping("/login")
    public ResponseEntity<?> login(@RequestBody AuthRequest request) {
        // 사용자 인증 로직
        String token = jwtTokenProvider.createToken(request.getUsername(), Collections.singletonList("USER"));
        return ResponseEntity.ok(new AuthResponse(token));
    }

    @GetMapping("/validate")
    public ResponseEntity<?> validateToken(@RequestParam String token) {
        if (jwtTokenProvider.validateToken(token)) {
            return ResponseEntity.ok("Valid token");
        }
        return ResponseEntity.status(HttpStatus.UNAUTHORIZED).body("Invalid token");
    }
}
문제 2: OAuth2 SSO를 활용한 사용자 프로필 정보 조회

@RestController
@RequestMapping("/user")
public class UserProfileController {

    @GetMapping("/profile")
    public ResponseEntity<?> getProfile(Authentication authentication) {
        UserDetails userDetails = (UserDetails) authentication.getPrincipal();
        Map<String, Object> response = new HashMap<>();
        response.put("username", userDetails.getUsername());
        response.put("roles", userDetails.getAuthorities());
        return ResponseEntity.ok(response);
    }
}
6.3. SSO 환경에서의 보안 고려 사항
6.3.1 학습자의 사고를 돕기 위한 질문
SSO 환경에서 토큰 탈취를 방지하기 위해 필요한 보안 조치는 무엇인가?

Access Token 및 Refresh Token의 저장 방식과 전달 방식을 고려해보라.
OAuth2 기반 SSO에서 Refresh Token이 필요 없는 경우가 있을까?

짧은 수명의 Access Token만으로도 충분한 시나리오를 생각해보라.
7. OAuth2와 JWT 사용 시 보안 고려 사항 및 Best Practices
7.1. OAuth2와 JWT의 보안 취약점
7.1.1 학습자의 사고를 돕기 위한 질문
OAuth2에서 Access Token이 탈취될 경우 발생할 수 있는 보안 위협은 무엇이며, 이를 방지하기 위한 방법은 무엇인가?

네트워크 가로채기 공격과 HTTPS 적용의 중요성을 고려해보라.
JWT가 너무 긴 유효 기간을 가지면 발생할 수 있는 보안 문제는 무엇인가?

유효 기간이 긴 경우 토큰 탈취 시 피해 범위를 고려해보라.
7.3. Refresh Token 보안 관리 및 갱신 정책
7.3.1 학습자의 사고를 돕기 위한 질문
Refresh Token이 서버에서 안전하게 관리되어야 하는 이유는 무엇인가?

Refresh Token이 탈취되었을 때의 보안 리스크를 고려해보라.
Refresh Token Rotation 기법이 보안 강화에 어떤 도움을 줄 수 있는가?

새로운 Refresh Token을 발급하는 과정과 기존 Refresh Token을 폐기하는 방식을 비교해보라.
7.4. OAuth2와 JWT 기반의 권한(Role) 관리
7.4.1 실습 문제에 대한 답안
문제 1: JWT 기반의 역할(Role) 부여 및 검증

@RestController
@RequestMapping("/admin")
public class AdminController {

    @GetMapping("/dashboard")
    @PreAuthorize("hasRole('ADMIN')")
    public ResponseEntity<String> getAdminDashboard() {
        return ResponseEntity.ok("Welcome to Admin Dashboard");
    }
}
문제 2: Spring Security에서 OAuth2 권한(Role) 검증

@Configuration
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
            .antMatchers("/admin/**").hasRole("ADMIN")
            .antMatchers("/user/**").hasRole("USER")
            .anyRequest().authenticated()
            .and()
            .oauth2Login();
    }
}
