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

<br>

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

<br>

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

<br>

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

## 참고 사이트 

> 구버전 https://next-auth.js.org/  
> 신버전(V5) https://authjs.dev/  
> 미들웨어 https://nextjs.org/docs/app/building-your-application/routing/middleware

<br><br>
