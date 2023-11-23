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
