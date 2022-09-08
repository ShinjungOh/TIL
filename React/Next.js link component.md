# Next.js Link Component

## Link  

### Link와 a 태그의 차이점

```javascript
// Link
<Link href="/posts/first-post">
    <a>첫번째 글</a>
</Link>

// a
<a href="/posts/first-post">첫번째 글(a tag)</a>
```

<br>

#### `Link`  
페이지 안에서 필요한 내용만 추가적으로 불러옴 -> 최적화   
* client side navigate
* prefetching

<br>

#### `a`
주소창에 새로운 주소를 입력해서 들어간 것과 같음
* 본 서비스 외부 링크로 연결할 때는 a 태그 사용 
* link component에 스타일을 줄 때는 a 태그에 줘야 함

<br><br>

## Client Side Navigate

브라우저에서 url을 직접 쳐서 이동하는 것과 달리, 자바스크립트 상에서 page 컴포넌트를 교체하는 것

* 확인 방법 : body에 background-color를 주고 navigate 해보기

<br><br>

## Code Splitting

next.js는 automatic code splitting을 제공 -> 성능 최적화
* 특정 페이지에 접근할 때, 해당 페이지를 그릴 때 필요한 chunk만 로드 
* 페이지 이동할 때, 목적지에 필요한 chunk만 로드

<br><br>

## Prefetching
뷰포트에 link 컴포넌트가 노출되었을 때, href로 연결된 페이지의 chunk를 로드 -> 성능 최적화

<br><br>

## 참고 사이트

> https://nextjs.org/docs/api-reference/next/link
