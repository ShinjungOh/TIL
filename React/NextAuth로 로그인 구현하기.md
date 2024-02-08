# Next 

## NextAuth

직접 구현해도 되지만, 넥스트에선 NextAuth를 많이 사용    
최근에 Auth.js로 이름이 바뀜 

넥스트, 스벨트, 솔리드 등도 지원

### 장점 

#### 1. Login Providers, 다양한 로그인 지원
> https://authjs.dev/getting-started/providers  

카카오, 네이버, 구글, 인스타그램 등 다양한 소셜 로그인 지원  
간편 로그인 구현하기 편함

#### 2. Credentials Provider
> https://authjs.dev/guides/providers/credentials

기본적인 아이디, 비밀번호 로그인도 지원  

#### 3. 로그인에 따른 쿠키 등을 관리해줌

<br><br>

## NextAuth로 로그인 구현하기

### 1. `auth.ts`, `middleware.ts` 파일 생성

app 디렉토리와 같은 위치에 파일 생성 

<br><br>

### 2. next-auth 설치

```bash
npm i next-auth@5

# 5버전이 아직 안나왔을 경우 
npm i next-auth@beta
```

```bash
# 역시 5버전이 아직 안 나왔으면 beta
npm i next-auth@beta @auth/core 
```

> 🚨 **500 서버 에러가 발생할 때 해결 방법**
> 
> `package.json`의 라이브러리 버전을 낮추기
> * next-auth 삭제 
> * npm i next-auth@5.0.0-beta.3 설치

```
“@auth/core”: “^0.19.0", 
“next”: “^14", 
“next-auth”: “^5.0.0-beta.3", 
“react”: “^18", 
“react-dom”: “^18"
```

<br><br>

### 3. `auth.ts` 파일 내용 작성

```ts
import NextAuth from "next-auth";
import CredentialsProvider from "next-auth/providers/credentials"

export const {
    handlers: {GET, POST},
    auth,
    signIn,
} = NextAuth({
  pages: {},
})
```

* 기본적인 틀 

<br><br>

### 4. `middleware.ts` 파일 내용 작성  

* `auth.ts`의 auth를 불러와서 미들웨어 역할을 하도록 함
* `config`는 미들웨어를 적용할 route
  * 미들웨어 적용할 route 목록을 matchers에 적으면 됨
  * 미들웨어는 넥스트에서 공식적으로 지원하는 기능

```ts
export { auth as middleware } from "./auth"

export const config = {
  matchers: ['/compost/tweet', '/home', 'explore', 'messages', '/search'],
}
```

* 로그인 해야 보이는 페이지들(미로그인 시 들어가지는/안 들어가지는 페이지 구분) 처리 
* Ex. 트위터에서는 미로그인 시, 메뉴가 비어있고 트렌드도 볼 수 없음

<br>

> 페이지 라우터 시절에는 페이지에 접근할 수 없는 유저를 처리하기 어려웠음   
> 넥스트에서는 **미들웨어** 기능을 지원함에 따라 그런 기능을 구현할 수 있게됨 
> * 앱 라우터에서는 미들웨어를 활용해서 페이지 접근 권한 등을 관리하기가 쉬워짐 
> * `middleware.ts`에서 미들웨어 함수를 만들고, 로그인한 사람만 접근할 수 있는 등의 로직 구현 
> * 매처에 해당되는 라우트에서는 이 함수가 페이지 렌더링 되기 전에 실행됨 

#### 미들웨어 함수

```
export { auth as middleware } from "./auth"
```

* 미들웨어 함수를 안 만들어도 export function middleware가 됨
* `auth.ts`에서 만들어 놓은 미들웨어 함수를 그대로 사용

<br><br>

### 5. 미들웨어, API 라우트, catch-all 라우트

* `middleware.ts` 파일에서는 NextAuth가 알아서 관리
  * `/api/auth` 관련 주소 등 관리
* auth 함수는 로그인 유무를 알아내는 용도
* `handlers: {GET, POST}`는 api 라우트

<br>

#### API 라우트

> https://nextjs.org/docs/app/building-your-application/upgrading/app-router-migration#api-routes

* 브라우저처럼 실제 주소가 됨
* 프론트 서버도 서버라서 API 호출로 쓸 수 있으며, DB 처리 가능
* 넥스트를 쓰면 백엔드 서버 없이도 모든걸 다 할 수 있음

```ts
// src/app/api/auth/[...nextauth]/route.ts

export { GET, POST } from "@/auth";
```

* `route.ts`를 만들면 이 파일이 api가 됨

<br>

#### catch-all 라우트

> https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes#catch-all-segments  
> 
> 🍀 src/app/api/auth/**[...nextauth]**/route.ts

* 디렉토리 이름의 `…` 도 의미가 있음
* [슬러그]에는 어떤 주소든 다 들어갈 수 있음
  * 칸을 마련하기 위한 이 칸의 이름
  
<br>

#### 서버 관리 

* 작은 서비스는 프론트/백엔드 서버 둘 다 두면 불편해서, 프론트 서버 하나에서 api 라우트, route.ts 만들어서 처리해도 됨 
* 프로젝트 규모가 커지면 프론트/백엔드 서버 나누는게 좋음
  * 장점 : 한 쪽 서버에 요청이 많아질 경우 한 쪽 서버만 늘리면 됨 
    * 같이 붙어있으면 서버를 둘 다 늘려줘야 함
    * 그래서 서버를 프론트/백엔드 기능별로 나누는 것

<br>

#### `.env` 파일 설정

* `AUTH_URL=http://localhost:포트번호` 추가
  * 배포에서도 똑같이 쓰이며, 배포 시에는 mock 서버가 아닌 **실제 서버 주소**로 교체할 것
  * NextAuth 사용할 때 오스 url `${process.env.AUTH_URL}/api/login`, 
* `AUTH_SECRET=시크릿키` 추가 
  * 유출되면 다른 사람인 것처럼 로그인 가능하기 때문에 절대 유출 금지 
  * 비밀번호라고 생각하면 됨 

<br><br>

### 6. next-auth로 로그인하기

> https://authjs.dev/getting-started/providers/credentials-tutorial

* 공식 문서의 credentials-tutorial 코드 사용

```ts
export const {
    handlers: {GET, POST},
    auth,
    signIn,
} = NextAuth({
    pages: { //직접 만든 페이지 등록
        signIn: '/i/flow/login',
        newUser: '/i/flow/signup',
    },
    providers: [
    CredentialsProvider({
        async authorize(credentials) {
            const authResponse = await fetch(`${process.env.AUTH_URL}/api/login`, {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify({
                    id: credentials.username,
                    password: credentials.password,
                }),
            })

            if (!authResponse.ok) {
                return null // 로그인 실패 이유 추가
            }

            const user = await authResponse.json()
            return user // 현재 로그인 여부, 로그인한 사람이 누구인가 등의 값을 가져옴
        },
    }),
    ]
});
```

* 로그인 시 authorize 코드가 실행
* credentials 안에 유저네임, 패스워드 등, 아이디 입력창에서 입력하는 정보가 들어있음

<br>

> ✅ **프로젝트에 따라 username, password 변경하기**
> 
> `username, password`로 고정되어 있기 때문에, 본인이 개발하는 프로젝트에서 이름을 변경하려면 추가 작업 필요  
> id와 username을 사용하는 프로젝트라면 바꿔주는 작업을 해야 함 

```ts
body: JSON.stringify({
    id: credentials.username,
    password: credentials.password,
})
```

<br><br>

### 7. 사용하기

#### 사용 환경

* 사용 방법은 동일, 서버/클라이언트 어느쪽에서 잘 돌아가는지의 차이
* 클라이언트 환경
  * `import {signIn} from “next-auth/react”;`
* 서버 환경
  * `import {signIn} from “@/auth”;` (직접 만든 것)

```tsx
"use client";

import {useRouter} from "next/navigation";
import {signIn} from "next-auth/react";

export default function LoginModal() {
  // 생략
  const onSubmit: FormEventHandler<HTMLFormElement> = async (e) => {
    e.preventDefault();
    setMessage('');
    try {
      await signIn("credentials", { // ✅
        username: id,
        password,
        redirect: false,
      })
      router.replace('/home');
    } catch (e) {
      console.error(e);
      setMessage('아이디와 비밀번호가 일치하지 않습니다.')
    }
  };
}
```

* `redirect: false`
  * true일 경우 서버쪽에서 리다이렉트를 하기 때문에, 클라이언트 컴포넌트에서는 router.replace 등으로 리다이렉트 처리 
* auth url이 `https`이면 배포모드로 설정되어서 secure 쿠키됨

<br>

#### 다양한 소셜 로그인

* 카카오 로그인 붙이고 싶으면 `auth.ts`에서
  * `CredentialsProvider({` 아래에 KakaoProvider 추가
* 로그인할 때도 "credentials" 대신에 
  * `signIn(“여기에“);` 해당하는 로그인 방법(kakao, google 등) 넣어서 호출
  
<br><br>

## 참고 사이트 

> 구버전 https://next-auth.js.org/  
> 신버전(V5) https://authjs.dev/  
> 미들웨어 https://nextjs.org/docs/app/building-your-application/routing/middleware  

<br><br>
