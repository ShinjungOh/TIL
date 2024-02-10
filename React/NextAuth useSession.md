# Next

## NextAuth

useSession을 사용하지 않으면 오류가 발생  

> 🚨Error: [next-auth]: `useSession` must be wrapped in a `<SessionProvider />`

<br><br>

## useSession

클라이언트 컴포넌트에서 쓰는 기능  
SessionProvider를 만들어서 레이아웃에 children을 감싸주기

* Provider들은 거의 다 클라이언트 컴포넌트

```tsx
<AuthSession>
    {children}
</AuthSession>
```

* `const session = await auth();`는 useSession의 서버 버전

<br>

### 예시 

```tsx
// 클라이언트 컴포넌트 
import {useSession} from "next-auth/react";  
const router = useRouter();
const session = useSession();

const {data: session} = useSession();

if (session?.user) {
    router.replace('/home');
    return null;
}
```

```tsx
// 서버 컴포넌트 
import {auth} from "@/auth"; 
const session = await auth();

if (session?.user) {
    redirect('/home');
    return null;
}
```

<br><br>

## 주의점 

* 🚨쿠키에 세션 토큰이 유출되지 않도록 조심할 것! 남이 나인 것처럼 로그인 가능
* NextAuth 설치하면 기본적으로 쿠키 두개가 생김
* 세션 토큰이 있어야만 로그인된 상태
* 네크워크탭에도 세션이 생기며, 요청이 보내지고 있음
  * 응답이 false, null이면 미로그인 상태

### 장점 

> CSRF 공격 : 로그인 쿠키를 빼가는 공격

NextAuth에서는 CSRF 공격으로 쿠키를 못 빼가도록 토큰으로 막아줌
쿠키 로그인의 가장 큰 보안 위협인 CSRF 공격을 알아서 막아주기 때문에 안전  

<br>

### `auth.ts`에 callback 추가

리다이렉트가 제대로 작동 안해서 auth에 callback 추가  
세션이 없을 때 어떤 url로 리다이렉트 시키는 코드

```tsx
callbacks:{
    async authorized({request, auth}) {
        if (!auth) {
            return NextResponse.redirect('http://localhost:3000/i/flow/login');
        }
        return true;
    }
},
```

* 이 방법 보다는 미들웨어에서 함수 추가하는게 더 고급진 방법

<br>

### 미들웨어에 함수 추가

```tsx
import {auth} from "@/auth";
import {NextResponse} from "next/server";

export async function middleware() {
    const session = await auth();
    
    if (!session) {
        return NextResponse.redirect('http://localhost:3000/i/flow/login');
    }
}
```

* 이 미들웨어 함수는 matcher 페이지들에만 동작
* 페이지에 접근할 때 `const session = await auth();`으로 현재 세션이 있는지 검사함

<br><br>

> https://next-auth.js.org/getting-started/client#usesession
