##PORT
한번에 둘 이상 연결하는 경우 <br>
PORT : 같은 IP 내에서 프로세스 구분. 서버 안에서 돌아가는 애플리케이션을 구분하는 것

TCP 세그먼트 : <u>출발지 PORT, 목적지 PORT</u>, 전송 제어, 순서, 검증 정보 등 <br>
<br>

<strong>TCP/IP 패킷</strong>
<br>

출발지 IP, PORT<br>
목적지 IP, PORT<br>
전송 데이터<br>

(IP = 아파트, PORT = 동호수)
<br><br>

* 0 ~ 65535 : 할당 가능
* 0 ~ 1023 : 잘 알려진 포트, 사용하지 않는 것이 좋음
    * FTP : 20, 21
    * TELNET : 23
    * HTTP : 80
    * HTTPS (HTTP에 보안 추가) : 443
      <br><br>
