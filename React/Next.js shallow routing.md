# Next.js routing

## Shallow Routing

getServerSideProps, getStaticProps 등을 다시 실행시키지 않고, url을 바꾸는 방법

<br>

💡 **현재 상태를 유지하면서 URL만 바꾸는 경우**  
사용자가 어떤 동작을 하고, 그 기록을 query로 남기고 싶을 때    
data fetching을 일으키고 싶지 않을 때  
(query로 남기면 새로고침을 해도 유지됨)
* Ex) <em>스크롤을 10페이지까지 내린 경우</em> 

<br><br>

## url을 바꾸는 3가지 방식

1️⃣ `location.replace("url")` -> 로컬 state 유지 ❌ (re-render), data-fetching 발생 ✔️ <br>
2️⃣ `router.push(url)` -> 로컬 state 유지 ✔️ , data-fetching 발생 ✔️ <br>
3️⃣ `router.push(url, as, { shallow: true })`️ -> 로컬 state 유지 ✔️, data-fetching 발생 ❌ <br>

* 동일한 페이지에서 query만 바뀌어야 함

<br><br>

## replace와 push의 차이점

### push

```js
import { useRouter } from 'next/router';

export default function Page() {
    const router = useRouter()
    
    const handleClick = (e) => {
    e.preventDefault()
    router.push('/about');
}
```

* router.push를 사용하면 stack의 맨 위에 새 경로가 추가됨

<br>

### replace

```js
import { useRouter } from 'next/router';

export default function Page() {
  const router = useRouter();

  return (
    <button type="button" onClick={() => router.replace('/home')}>
      Click me
    </button>
  )
}
```

* router.replace를 사용하면 스택 상단을 덮어 씀
* 사용자가 유효하지 않은 경로로 이동하면 router.replace를 통해 이동하지 못하게 할 수 있음
* 뒤로가기 시 해당 페이지가 보이지 않도록 처리 (로그아웃 등)




<br><br>

## 참고 사이트

> https://nextjs.org/docs/routing/shallow-routing  
> https://nextjs.org/docs/api-reference/next/router
