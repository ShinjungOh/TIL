## URI
<strong>URI</strong><br>
Uniform Resource Identifier <br>

<strong>U</strong>niform 리소스를 식별하는 통일된 방식 <br>
<strong>R</strong>esource 자원, URI로 식별할 수 있는 모든 것 (제한 없음) <br>
<strong>I</strong>dentifier 다른 항목과 구분하는데 필요한 정보 <br>

<br>
<strong>URI</strong> : 리소스를 식별한다. URI는 로케이터(locator), 이름(name) 또는 둘 다 추가로 분류될 수 있다. <br>
<strong>URL</strong> : 리소스의 위치 (Resource Locator) <br>
<strong>URN</strong> : 리소스의 이름 (Resource Name) <br>
<br>

* 위치는 변할 수 있지만, 이름은 변하지 않음
* Ex) urn : isbn : 98327480234 (어떤 책의 isbn URN) 
* URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음 <br>

=> URI와 URL를 같은 의미로 설명 

<br>


<strong>전체 문법</strong>
<br>

scheme://[userinfo@]host[:port][/path][?query][#fragment] 
https://www.google.com:443/search?q=hello&hl=ko <br>

  * 프로토콜(https) 
  * 호스트명(www.google.com) 
  * 포트 번호(443)
  * 패스(/search)
  * 쿼리 파라미터(q=hello&hl=ko)

<br>

* scheme (https)
  * 주로 프로토콜 사용 
  * 프로토콜: 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙 
    * 예) http, https, ftp 등등 
  * http는 80 포트, https는 443 포트를 주로 사용, 포트는 생략 가능
  * https는 http에 보안 추가 (HTTP Secure)
  
<br>

* userinfo
  * URL에 사용자정보를 포함해서 인증
  * 거의 사용하지 않음

<br>

* host (www.google.com)
  * 호스트명
  * 도메인명, IP 주소를 직접 사용가능

<br>

* PORT (:443)
  * 접속 포트
  * 일반적으로 생략, 생략시 http는 80, https는 443

<br>

* path (search)
  * 리소스 경로(path), 계층적 구조 
  * 예) <br>
  • /home/file1.jpg <br>
  • /members <br>
  • /members/100, /items/iphone12 <br>

<br>

* query (?q=hello&hl=ko)
  * key=value 형태 
  * ?로 시작, &로 추가 가능 ?keyA=valueA&keyB=valueB 
  * query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터, 문자 형태

<br>

* fragment
  * https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started.html#getting-started-introducing-spring-boot 
  * fragment 
  * html 내부 북마크 등에 사용 
  * 서버에 전송하는 정보 아님