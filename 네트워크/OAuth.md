# OAuth

## 개념

OAuth를 사용하면 사용자가 자신의 데이터를 제3자에게 제공할 수 있음    
인증과정에 참여하는 3자가 어떻게 서로를 신뢰할지에 대한 고민으로 시작된 기술

* 사용자의 데이터를 제3자에게 직접 제공하는 것이 아니라, 제3자가 사용자의 데이터에 접근할 수 있는 권한을 부여하는 것
* 나의 서비스와 이용하고자하는 서비스가 안전하게 상호작용할 수 있게 됨  
* OAuth을 통해 accessToken을 발급받아서 사용자의 데이터에 접근할 수 있음
* OAuth는 애플리케이션 기술(PHP, Python, Ruby, JavaScript, Node.js, Java 등)을 이용해 구현됨

![OAuth.png](..%2FImages%2FOAuth.png)

### accessToken의 장점

1. 사용자의 ID/비밀번호가 아님
2. 제3자의 서비스에서 나의 서비스에 필요한 필수적인 기능만 부분적으로 허용하는 비밀번호

<br><br>

## 제3자의 역할

* Resource Owner : 사용자
* Resource Server : 리소스 제공자 (구글, 페이스북 등), 데이터를 가지고 있는 서버  
  * authorization server : 인증 담당으로 accessToken을 client에게 보내줌 (구글의 인증 담당 서버)
  * 공식문서에서는 두 가지를 구분하지만, 합쳐서 간략하게 리소스 서버로 부름 
* Client : 서드 파티 서비스 (나의 서비스)
  * 리소스 서버로부터 정보를 가져가는 클라이언트

<br><br>
 
## OAuth 등록 절차 

OAuth를 이용해서 Resource Server에 접속하려면 Resource Server에 등록하는 과정이 필요

### OAuth2 클라이언트가 레지스터 서버에 등록하기 위한 필수요소

1. Client ID : 나의 서비스를 식별하는 ID
2. Client Secret : 비밀번호(유출 X) 
3. Authorized redirect URL : 리소스 서버가 Authorized Code를 전달해줄 URL 
  * 다른 주소에서 요청하면 무시됨

<br><br>

## Resource Owner의 승인

OAuth의 첫번째 절차는 Resource Owner가 Resource Server에게 Client의 접근을 승인한다는 것을 알려줘야 함

사용자가 동의해야(버튼 클릭 등) 다음 과정으로 진행할 수 있음 

```bash
# 버튼 링크 예시

https://resource.server/
    ?clent_id=1
    &scope=B,C # 사용하려는 리소스 서버의 기능(A, B, C, D 중 2개 사용할 경우)
    &redirect_url=https://client/callback
```

1. 리소스 오너가 리소스 서버로 접속하면(버튼 클릭해서)
2. 리소스 서버가 '리소스 오너(유저)가 **로그인**이 되어있는지' 확인 후, 
3. 로그인하지 않았으면 로그인하라는 화면을 보여줌 
4. 로그인을 했으면 clent_id과 같은 **id** 값이 있는지 확인 후, **리다이렉트 url**을 확인 
   * url이 다르면 작업 종료 
6. url이 같으면 리소스 오너에게 권한을 요청하는 화면을 보여줌 
7. 허용하면 user Id가 scope b, c 작업을 허용하는 것에 동의헸다는 정보를 리소스 서버의 DB 등에 저장

<br><br>

## Resource Server의 승인

> 엑세스 토큰을 발급하기 전 승인 단계

1. 리소스 서버는 클라이언트가 등록된 클라이언트가 맞는지 확인이 필요 
2. 리소스 오너를 통해 클라이언트에게 Authorization code를 전달 
3. 이 값을 받은 클라이언트는 이 값과 클라이언트 secret의 값을 리소스 서버로 전송 
4. 클라이언트의 신원을 리소스 오너에게 증명

```bash
# 리소스 서버가 리소스 오너에게 Authorization code를 전달

Location: https://client/callback?code=임시비밀번호
```

* 임시 비밀번호 = Authorization code

리소스 오너는 이 주소로 이동하게 됨  
code 값에 의해서 클라이언트는 Authorization code를 알게 됨  
클라이언트는 다음의 주소로 리소스 서버에 직접 접속   

```bash
https://resource.server/token
    ?grant_type=authorization_code
    &code=임시비밀번호
    &redirect_url=https://client/callback
    &clent_id=1
    &client_secret=2 # 중요 
```

리소스 서버는 정보를 확인하고 이 코드가 일치하면 엑세스 토큰을 발급 

<br><br>

## AccessToken 발급

> OAuth의 핵심인 access token의 값을 발급 받는 과정

OAuth의 목적은 엑세스 토큰을 발급하는 것

1. 리소스 서버는 인증이 끝나면 Authorization code 값을 지움 
   * 그래야 다시 인증을 안하기 때문
2. 리소스 서버는 엑세스 토큰을 발급
3. 엑세스 토큰의 클라이언트에게 `AccessToken=4`라고 전달
4. 클라이언트는 엑세스 토큰을 저장
5. 리소스 서버는 클라이언트가 엑세스 토큰으로 접근하면, 리소스 오너의 정보에 대해 특정 기능을 보장

Resource Server가 Client에게 Access Token을 발급하고 Client가 Server에게 Access Token을 요청하면 Server에서 허용된 기능을 제공해줌

![OAuth_흐름.png](..%2FImages%2FOAuth_%ED%9D%90%EB%A6%84.png)

* 리프레쉬와 엑세스 토큰 만료에 대한 이미지

<br><br>

## 참고 사이트 

> [OAuth 2.0 이해하기: 인증과 인가의 현대적 접근](https://f-lab.kr/insight/understanding-oauth-2-0?gad_source=1&gclid=CjwKCAiA0bWvBhBjEiwAtEsoW0bgc9V0Pn1QGgNdyNCNNHcGBLH909ocC0x9r3YmtxmyQYzH88Q7yBoCVw0QAvD_BwE)  
> https://datatracker.ietf.org/doc/html/rfc6750
