# HTTP

## CORS

교차 출처 리소스 공유 (**C**ross-**O**rigin **R**esource **S**haring)

CORS는 HTTP의 일부로, 어떤 호스트에서 자신의 콘텐츠를 불러갈 수 있는지 서버에 지정할 수 있는 방법  
출처가 다른 곳이어도 괜찮으며, 리소스를 공유할 것이라고 서버(리소스를 제공하는 곳) 에서 알려줌

* **REST API 서버**에서 `Headers`에 `Access-Control-Allow-Origin` 속성을 추가
* **Express**에서는 `CORS 미들웨어` 를 설치해서 사용

추가 HTTP 헤더를 사용해, 한 출처에서 실행 중인 웹 애플리케이션이 **다른 출처의 선택한 자원에 접근**할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제  
웹 애플리케이션은 리소스가 자신의 **출처(Origin, 도메인, 프로토콜, 포트)** 와 다를 때 교차 출처 HTTP 요청을 실행

<br>

### 교차 출처 요청의 예시

`XMLHttpRequest`와 `Fetch API`는 **동일 출처 정책**을 따름 

> Ex. `https://domain-a.com`의 프론트엔드 JavaScript 코드가 **XMLHttpRequest**를 사용해 `https://domain-b.com/data.json` 을 요청하는 경우

보안 상의 이유로, **브라우저는** 스크립트에서 시작한 **교차 출처 HTTP 요청을 제한**   

* 이 API를 사용하는 웹 애플리케이션은 **자신의 출처와 동일한 리소스만 불러올 수 있음**
* 다른 출처의 리소스를 불러오려면 그 출처에서 **올바른 CORS 헤더를 포함한 응답을 반환**해야 함 

<br>

#### CORS 표준

웹 브라우저에서 해당 정보를 읽는 것이 `허용된 출처`를 **서버**에서 설명할 수 있는 `새로운 HTTP 헤더를 추가`함으로써 동작

#### CORS 명세

> 서버 데이터에 사이드 이펙트를 일으킬 수 있는 HTTP 요청 메소드(GET을 제외한 HTTP 메소드)에 대해

* 브라우저가 요청을 `OPTIONS` 메소드로 **프리플라이트**(preflight, 사전 전달)하여 지원하는 메소드를 요청하고,
서버의 `허가`가 떨어지면 실제 요청을 보내도록 요구 
* 서버는 클라이언트에게 요청에 `인증정보`(쿠키, HTTP 인증)를 함께 보내야 한다고 알려줄 수도 있음

<br><br>

## HTTP 헤더

클라이언트와 서버가 요청/응답으로 부가적인 정보를 전송할 수 있도록 함  
HTTP 헤더는 대소문자를 구분하지 않는 `이름`과, ':' 다음에 오는 `값`으로 구성

#### CORS 관련 HTTP 헤더

> 교차 출처 리소스 공유 기능을 사용하기 위한 방법  

| 헤더                            | 기능                                                         |
|-------------------------------|------------------------------------------------------------|
| Access-Control-Allow-Origin   | 응답이 공유될 수 있는지를 나타냄                                         |
| Access-Control-Allow-Credentials | credentials 플래그가 true일 때 요청에 대한 응답이 노출될 수 있는지를 나타냄         |
| Access-Control-Expose-Headers | 헤더의 이름을 나열하여 어떤 헤더가 응답의 일부로 노출될 수 있는지를 나타냄                 |
| Access-Control-Allow-Methods| preflight 요청에 대한 응답으로 리소스에 접근할 때 허용되는 메소드를 명시합니다.          |
| Origin    | cross-site 접근 요청, preflight request의 출처를 나타냄               |
| Access-Control-Request-Headers | 실제 요청이 있을 때 사용될 HTTP 헤더를 서버에 알리기 위한 preflight 요청을 보낼 때 사용  |
| Access-Control-Request-Method | 실제 요청이 있을 때 사용될 HTTP 메소드를 서버에 알리기 위한 preflight 요청을 보낼 때 사용 |

<br>

### HTTP 요청 헤더

**클라이언트**가 HTTP 요청을 발행할 때 사용할 수 있는 헤더  
서버를 호출할 때 설정됨 

* Origin 
* Access-Control-Request-Method 
* Access-Control-Request-Headers

<br>

### HTTP 응답 헤더

**서버**가 접근 제어 요청을 위해 보내는 HTTP 응답 헤더

* Access-Control-Allow-Origin
* Access-Control-Expose-Headers
* Access-Control-Max-Age 
* Access-Control-Allow-Credentials
* Access-Control-Allow-Methods 
* Access-Control-Allow-Headers

<br><br>

## 동일 출처 정책

Same Origin Policy

웹 브라우저가 가진 기본 **보안 정책**  
어떤 출처에서 불러온 문서나 스크립트가 **다른 출처**에서 가져온 리소스와 상호작용하는 것을 **제한**하는 보안 방식   
잠재적 악성 문서를 격리해서 공격을 줄이는 데 도움됨

Ex. 악성 웹사이트가 브라우저에서 자바스크립트를 실행해,
`(사용자가 로그인한) 타사 웹메일 서비스`나 `회사 인트라넷 (공용 IP 주소가 없어 공격자의 직접적인 접근으로부터 보호)`에서
데이터를 읽고 공격자에게 전달하는 것을 방지

<br>

### 동일 출처 정책을 어겼을 경우 

> 🚨 **에러 메시지**
> 
> Access to fetch at 'http://localhost:3000/products' from origin 'http://localhost:8080' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource. If an opaque response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disabled.
>
> 개발자 도구의 네트워크 탭에서 살펴보면 서버에서 response 응답은 오지만(🟢 200 OK)  
> 동일 출처가 아니기 때문에 **브라우저에서** 막힘 → **오류 발생**


웹 브라우저는 `Same Origin Policy`에 따라 **웹 페이지와 리소스를 요청한 곳**(여기서는 REST API 서버)이 **서로 다른 출처**(포트까지 포함)일 때, 서버에서 얻은 결과를 **사용할 수 없게 막음**

⚠️ 서버에 요청하고 응답을 받아오는 것까지는 이미 진행이 완료된 상황

* 잠재적으로 해로울 수 있는 문서를 분리해, 공격받을 수 있는 경로를 줄여줌
* **CORS**를 사용해 `교차 출처 접근을 허용`할 수 있음

<br><br>

## 참고 사이트 

> https://developer.mozilla.org/ko/docs/Web/Security/Same-origin_policy  
> https://developer.mozilla.org/ko/docs/Web/HTTP/CORS
