# HTTP 상태코드 

## 3XX Redirection

300번대 상태코드는 요청을 완료하려면 **추가 행동**이 필요

<br><br>

## 304 Not Modified

클라이언트 리디렉션 응답 코드 `304 Not Modified`는 요청된 리소스를 재전송할 필요가 없음을 나타냄   
**캐시된 자원으로의 암묵적인 리디렉션**

### 특징 

* **캐시**를 목적으로 사용
* 클라이언트에게 **리소스가 수정되지 않았음**을 알려줌
* 클라이언트는 로컬 PC에 저장된 **캐시를 재사용** (캐시로 리다이렉트)
* 304 응답은 응답에 메시지 바디를 포함하면 안 됨 (로컬 캐시를 사용해야 하므로)
* 조건부 `GET`, `HEAD` 요청 시 사용

<br>

### GET

HTTP `GET` 메소드는 특정한 리소스를 가져오도록 요청  
GET 요청은 데이터를 가져올 때만 사용해야 함 

<br>

### HEAD

HTTP `HEAD` 메소드는 특정 리소스를 `GET` 메소드로 요청했을 때 돌아올 헤더를 요청

* HEAD 메소드에 대한 응답은 본문을 가져선 안되며, 본문이 존재하더라도 무시해야 함   
  * `Content-Length`처럼 본문 콘텐츠를 설명하는 개체 헤더는 포함할 수 있음 
* 개체 헤더는 비어있어야 하는 HEAD의 본문과는 관련이 없고, 대신 GET 메소드로 동일한 리소스를 요청했을 때의 본문을 설명
* HEAD 요청의 응답이 **캐시했던 이전 GET 메소드의 응답**을 유효하지 않다고 표시할 경우, 
새로운 `GET` 요청을 생성하지 않더라도 **캐시를 무효화**

<br><br>

## 명세

`조건부 GET, HEAD` 요청이 수신되었으며, 조건이 false로 평가되지 않았다면, **200(OK) 응답이 발생**했음을 나타냄   
조건부 요청을 한 클라이언트가 이미 유효한 표현을 가지고 있음을 요청이 나타내기 때문에, 서버가 대상 리소스의 표현을 전송할 필요가 없음

→ 서버는 `200(OK) 응답`의 내용인 것처럼 **저장된 표현을 사용하도록 클라이언트를 리디렉션**

304 응답을 생성하는 서버는, 동일한 요청에 대한 200(OK) 응답으로 전송되었을 때 다음 `헤더 필드` 중 하나를 생성해야함

* Content-Location, Date, ETag, Vary
* 캐시 제어 및 만료
* 304 응답의 목표는, 수신자가 이미 하나 이상의 **캐시된 표현을 가지고 있을 때 정보 전송을 최소화**하는 것이므로,
  해당 메타데이터가 캐시 업데이트를 안내할 목적으로 존재하지 않는 한, 발신자는 위의 필드 이외의 표현 메타데이터를 생성하면 안됨

조건부 요청이 아웃바운드 클라이언트에서 시작된 경우(Ex. 자체 캐시가 있는 사용자 에이전트가 공유 프록시에 조건부 GET을 보내는 경우)
프록시는 `304 응답`을 해당 클라이언트에 전달해야 함   
304 응답은 헤더 섹션이 끝나면 종료되며, 콘텐츠나 트레일러를 포함할 수 없음

<br><br>

## 참고 사이트

> https://developer.mozilla.org/ko/docs/Web/HTTP/Status/304
