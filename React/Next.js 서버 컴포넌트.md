# Next.js App Router

## 서버 컴포넌트

[server components](https://nextjs.org/docs/app/building-your-application/rendering/server-components)

서버 컴포넌트는 React v18에서 추가된 기능  
리액트 서버 컴포넌트를 사용하면 서버에서 렌더링하고 선택적으로 캐시할 수 있는 UI를 작성할 수 있음 


### 서버 컴포넌트 에러 

![](../Images/Next_서버컴포넌트에러.png)

> 🚨 You're importing a component that needs useState. It only works in a Client Component but none of its parents are marked with "use client", so they're Server Components by default.
Learn more: https://nextjs.org/docs/getting-started/react-essentials

useState는 클라이언트 컴포넌트에서만 동작하는데 지금은 서버 컴포넌트를 사용하고 있다는 오류

* 기본적으로 프로젝트의 모든 컴포넌트는 서버 컴포넌트 (page.tsx, layout.tsx 등)
* Next.js 서버에서 돌고 있음
* async로 비동기 컴포넌트를 만들 수도 있음

<br><br>

### 주의점 

⚠️ 서버 컴포넌트에서는 useEffect, useState, useRouter 등의 hook을 사용할 수 없음  
-> 클라이언트 컴포넌트로 바꿔줘야함(hook은 클라이언트 컴포넌트에서만 작동)   
`“use client”` 를 붙이면 클라이언트 컴포넌트로 간단히 변환 

* 이벤트 리스너(onClick 등)가 있으면 `use client` 사용해야 함 
* 서버 컴포넌트는 클라이언트 컴포넌트를 import 해도 되는데, 그 반대는 불가

