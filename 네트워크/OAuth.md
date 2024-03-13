# OAuth

## 개념

OAuth를 사용하면 사용자가 자신의 데이터를 제3자에게 제공할 수 있음  

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

oauth2 클라이언트가 레지스터 서버에 등록하기 위한 필수요소 
* Client ID : 나의 서비스를 식별하는 ID
* Client Secret : 비밀번호(유출 X) 
* Authorized redirect URL : 리소스 서버가 Authorized Code를 전달해줄 URL 
  * 다른 주소에서 요청하면 무시됨

<br><br>

## Resource Owner의 승인

OAuth의 첫번째 절차는 Resource Owner가 Resource Server에게 Client의 접근을 승인한다는 것을 알려줘야 함





<br><br>

## 참고 사이트 

> [OAuth 2.0 이해하기: 인증과 인가의 현대적 접근](https://f-lab.kr/insight/understanding-oauth-2-0?gad_source=1&gclid=CjwKCAiA0bWvBhBjEiwAtEsoW0bgc9V0Pn1QGgNdyNCNNHcGBLH909ocC0x9r3YmtxmyQYzH88Q7yBoCVw0QAvD_BwE)
