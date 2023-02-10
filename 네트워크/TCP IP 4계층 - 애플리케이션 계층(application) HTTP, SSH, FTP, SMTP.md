# TCP/IP 4계층 

## 애플리케이션 계층(application)

HTTP, SMTP, SSH, FTP가 대표적  
웹 서비스, 이메일 등 서비스를 실질적으로 사람들에게 제공하는 층

<br><br>

## HTTP

HTTP(Hypertext Transfer Protocol)은 처음에는 `서버와 브라우저간`에 데이터를 주고 받기 위해 설계된 프로토콜   
지금은 브라우저 뿐만 아니라 `서버와 서버간` 통신할 때도 많이 이용

### 특징 

1. HTTP는 헤더를 통한 확장이 쉬움
   * 헤더값에다가 어떠한 값을 넣어서 HTTP요청을 할 때 쉽게 다른 값을 추가할 수 있음

2. HTTP는 stateless (상태를 저장하지 X)
   * 동일한 연결에서 연속적으로 수행되는 두 요청 사이에 연속적인 상태(state)값은 없음  
   
<br><br>

## SSH

SSH(Secure SHhell Protocol)는 보안되지 않은 네트워크에서,  
네트워크 서비스를 안전하게 운영하기 위한 `암호화 네트워크 프로토콜`  

Ex. 사용자에게 코드가 보여지지 않으면서, 내 PC의 코드를 안전하게 운반하려고 할 때

### 예시

```
ssh <pem>  <user>@<serverIP>
```

AWS 내의 EC2에 접근하는 모습  
1. 보통 프라이빗 키가 있는 경로에서 이런식으로 키를 명시하고 실행
   * AWS에서 pem 키를 받고, pem 키를 기반으로 인증
2. 접근해서 리눅스 명령어를 통해 CLI 환경에서 작업을 진행
3. SCP를 이용해서 SSH를 이용해 파일 전송 가능  
```
scp <source> <destination>
```

<br><br>

## FTP

FTP (File Transfer Protocol)는 노드와 노드간의 `파일을 전송`하는데 사용되는 프로토콜   
지금은 파일을 암호화해서 전송하는 FTPS 또는 SFTP로 대체되고 있음

Ex. 로컬 PC에서 원격서버로 파일을 보낼 때   
Ex. 파일질라 : 대표적인 FTP 소프트웨어  

<br><br>

## SMTP
인터넷을 통해 `메일을 보낼 때` 사용되는 프로토콜(Simple Mail Transfer Protocol)  

Ex. Nodemailer 라이브러리 : JS를 기반으로 SMTP를 통해 메일을 보낼 수 있는 라이브러리 
* node.js를 통해 메일을 보낼 때

```js
 // create reusable transporter object using the default SMTP transport
let transporter = nodemailer.createTransport({
   host: "smtp.ethereal.email", 
   port: 587,
   secure: false, // true for 465, false for other ports 
   auth: {
       user: testAccount.user,  // generated ethereal user
       pass: testAccount.pass, // generated ethereal password
   }, 
});
```
