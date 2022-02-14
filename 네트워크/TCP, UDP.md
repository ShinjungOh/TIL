##TCP, UDP
<strong>인터넷 프로토콜 스택의 4계층</strong>
* 애플리케이션 계층 : HTTP, FTP
* 전송 계층 : TCP, UDP
* 인터넷 계층 : IP
* 네트워크 인터페이스 계층
  <br>
  <br>

<strong>TCP/IP 패킷 정보</strong>
<br>

1. IP 패킷 : 출발지 IP, 목적지 IP, 기타 <br>
    2. TCP 세그먼트 : 출발지 PORT, 목적지 PORT, <u>전송 제어, 순서, 검증 정보 등</u> <br>
        3. 전송 데이터<br>

=> IP만으로 해결되지 않던 데이터 전달 보증, 순서 제어 문제 등이 해결
<br><br>

<strong>TCP 특징</strong>
<br>

전송 제어 프로토콜(Teansmission Control Protocol)
<br>
* 연결 지향 - TCP 3 way handshake(가상 연결)
* 데이터 전달 보증 (메시지를 받지 못했을 때 알 수 있다)
* 순서 보장

=> 신뢰할 수 있는 프로토콜<br>
=> 현재는 대부분 TCP 사용

<br>
<strong>TCP 3 way handshake</strong>
<br>
클라이언트와 서버 간의 가상 연결
<br><br>
1. [클라이언트] SYN (접속 요청) -> 2. [서버] SYN + ACK (요청 수락) -> 3. [클라이언트] ACK (+ 4. 데이터 전송) <br>
<br>
<br>
<strong>UDP 특징</strong>
<br>

사용자 데이터그램 프로토콜(User Datagram Protocol)<br>

* TCP와 같은 계층, IP의 상위 계층
* 기능이 거의 없음
* 연결 지향, 데이터 전달 보증, 순서 보장 X
* 단순하고 빠름 (TCP는 방대하고 느림)
* IP와 거의 동일 + <u>PORT</u> + 체크섬 정도만 추가
* 애플리케이션에서 추가 작업 필요
* 요새 뜨는 중
  <br><br>
