# React

## useSocket으로 웹소켓 연결하기

### 설치하기

```
npm i socket.io-client@4
```

서버에서 4버전을 사용하면 클라이언트에서도 버전을 일치시켜주기 

### 웹소켓의 활용

* 웹사이트에 접근해 있다가 실시간으로 알림이 왔을 때, 실시간으로 새 게시글이 등록됐을 때  
  * HTTP 요청을 보내지 않아도 서버로부터 먼저 데이터를 받을 수 있음 
* 원래는 서버에 요청을 보내고 응답을 받아서 화면에 그려줬다면,
  * 웹소켓을 한번 연결을 해두면 따로 요청을 보내지 않아도 서버로부터 데이터를 받아올 수 있음
* 메세지 외에 다른곳에서도 사용 가능  
* 소켓io는 연결 실패했을 때 재시도를 알아서 해주기 때문에 편리

### useSocket

useSocket은 Socket과 Disconnect 함수를 리턴하는 커스텀 훅  
Disconnect는 웹소켓 연결을 종료하는 함수

```tsx
// 서버와 웹소켓을 연결하는 주소
io(`${process.env.NEXT_PUBLIC_BASE_URL}/massages`);
```

```tsx
transports: ['websocket'], // 풀링 안하고 웹소켓만 쓰겟다는 옵션
```
    
* 소켓Io는 웹소켓을 지원하지만 웹소켓이 없는 구형 브라우저에서는 HTTP 폴링을 지원
  * 폴링 : 주기적으로 요청을 보내는 것 
  * 웹소켓이 없었을 때는 주기적으로 서버한테 새로운 데이터를 묻고 응답 받고 먼저 요청을 보내야 헸음 

<br><br>

## 주의점

### 서버 컴포넌트에서의 소켓 IO

소켓io를 서버 컴포넌트에서 쓰면 메모리 누수(메모리가 자꾸 올라가는 것)문제가 있을 수 있음  
서버 컴포넌트에서는 소켓 IO가 쓰이지 않게 주의  
-> 클라이언트 컴포넌트 별도로 만들어서 사용하기 등의 방법이 있음

### 소켓 공유하기

```tsx
let socket: Socket | null; // 안티패턴이지만 커스텀 훅 간에 공유할 데이터는 여기에 넣어두기 (공유할 때는 어쩔 수 없음)

export default function SampleComponent() {
// ⚠️ 소켓을 공유하기위해서는 state가 아니라 위에다가 적어줘야 함  
    const [socket, setSocket] = useState<Socket | null>(null);     
    
    return //
}
```

매번 스테이트를 새로 생성하는 문제  
소켓이 공유되는 게 아니고 그때마다 상태가 다시 생성  
-> 공유할 데이터는 이렇게 하면 안 됨 
 

```
socket?.emit('sendMessage');
```

'' 안의 내용은 서버와의 약속이라 바뀔 수 있음

<br><br>

## 브라우저 개발자 도구에서 웹소켓 확인하기

![웹소켓_네트워크.png](..%2FImages%2F%EC%9B%B9%EC%86%8C%EC%BC%93_%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC.png)

### SID

* SID가 소켓의 ID 
* 서버와 웹소켓 연결을 맺을 때마다 서버는 고유의 아이디를 내려보내줌 
* 한 페이지에서 웹소켓 연결을 여러 개 맺을 수도 있음 
  * 메시지 페이지에서는 메세지스로 워크스페이스에서 연결 맺기 
  * 알림 페이지에서는 노티피케이션 네임스페이스로 연결 맺기
* 네임스페이스 연결 후에 로그인했다고 뜨면 성공

### 로그인 

> 연결을 맺었을 때 로그인을 무조건 해야함

* 소켓 아이디가 나의 아이디와 연결되어 있다는 것을 웹소켓이 모르기 때문
* HTTP에서는 로그인이 되어있어서 쿠키를 주고받으면서 로그인이 되어있음
* 웹소켓은 다른 프로토콜이기 때문에 로그인이 안 되어있음

```tsx
useEffect(() => {
    if (socket?.connected && session?.user?.email) {
        socket?.emit('login', {
            id: session?.user?.email,
        });
    }
}, [session]);
```

<br><br>

## 참고 사이트 

> https://hooks.reactivers.com/use-socket  
> https://www.npmjs.com/package/socket.io-client
