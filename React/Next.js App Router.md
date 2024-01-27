# Next.js App Router

## Routing

페이지에 관한 것은 app 디렉토리의 하위에 생성  
import의 @ 는 src를 나타냄   
넥스트의 단점은 폴더 구조로 주소 구조를 만들기 때문에, 폴더가 많아지거나 폴더 구조가 깊어지거나 등의 문제를 겪을 수밖에 없음 

### 디렉토리 이름

* (소괄호) : ✅ 주소창에 관여하지 않음, 그룹을 만들 수 있음, 레이아웃
* [대괄호] : 다이나믹 라우팅, 슬러그(slug)
* _폴더 : 폴더 정리용 프라이빗 폴더 

<br>

### private folder(_폴더)

[private folders](https://nextjs.org/docs/app/building-your-application/routing/colocation#private-folders)

디렉토리 이름에 언더바를 붙이면 프라이빗 폴더가 됨  
폴더가 비공개 구현 세부 사항이므로 폴더와 모든 하위 폴더를 라우팅에서 제외

* ✅ 주소창에 뜨지 않음, 폴더 정리용

<br>

### layout.js

[layout.js](https://nextjs.org/docs/app/api-reference/file-conventions/layout)

경로 간에 공유되는 UI

* 레이아웃, 페이지는 함수 이름이 중요하지 않음, export default만 해주면 됨

<br>

### page.js

[page.js](https://nextjs.org/docs/app/api-reference/file-conventions/page)

페이지는 경로에 고유한 UI

* 레이아웃, 페이지는 함수 이름이 중요하지 않음, export default만 해주면 됨

<br>

### template.js

[template.js](https://nextjs.org/docs/app/api-reference/file-conventions/template)

페이지 넘길 때 레이아웃도 리렌더링 되게 하고 싶으면 template.tsx 사용

* layout: 리렌더링 x
* template:  리렌더링 ㅇ
  * 페이지 넘길때마다 무언가를 기록해야할 때 (GA 등)
* 둘이 공존하면 안됨

<br>

### Parallel Routes

[Parallel Routes](https://nextjs.org/docs/app/building-your-application/routing/parallel-routes)

뒤 페이지 그대로 두고 모달 띄우는 방법, 병렬 라우팅    
같은 폴더에 있어야 작동하며, 레이아웃에서 사용 가능  
**두가지 화면을 한 페이지에서 보여줄 수 있음**   
디렉토리 이름에 @를 붙이면 패러렐 라우트를 할 수 있음  

* @ 뒤의 이름(Ex. modal)이 레이아웃의 props가 됨
* @ 아래로 경로 맞추어야 함
* ✅ @ 는 주소에 해당하지 않음 

<br>

### default.tsx

패러렐 라우트에 대한 기본값, 패러렐 라우트가 필요 없을 때 보여줄 페이지   
⚠️ 없으면 오류 발생  

```tsx
// 주소가 z.com (localhost:3000) 일 때

return (
    // ... 
    {children} // children -> page.tsx
    {modal} // modal -> @modal/default.tsx
)
```

패러렐 라우트에서 모달을 2개 이상 띄우고 싶으면 `@modal2` 등의 폴더 생성하고, `default.tsx` 생성

<br>

### useSelectedLayoutSegment(s)

[useSelectedLayoutSegment](https://nextjs.org/docs/app/api-reference/functions/use-selected-layout-segment)

`useSelectedLayoutSegment`은 내가 현재 어떤 라우터에 있는지 알 수 있는 넥스트의 훅  
호출된 레이아웃 보다 한 수준 아래에 있는 활성 경로 세그먼트를 읽을 수 있는 클라이언트 구성 요소 훅    
현재 레이아웃에 있는 세그먼트, 내 현위치를 문자열로 반환  
`useSelectedLayoutSegments`는 자식들까지 전체를 다 반환

<br>

### Intercepting Routes

[Intercepting Routes](https://nextjs.org/docs/app/building-your-application/routing/intercepting-routes)

서로 주소가 다르지만 같이 뜰 수 있게 하는 방법   
넥스트13 앱 라우터에서 가장 어려운 부분

* (..) 이나 (.) 은 브라우저 주소 기준
* **클라이언트에서 라우팅**할 때만 인터셉트 라우팅이 적용됨

#### 예시 

* 패러렐 라우터가 인터셉팅을 해서 홈 화면에서 모달이 띄워지는 것처럼 보임
  * 원래는 `i/flow/login/page.tsx`으로 넘어가야 함
  * 인터셉팅을 하면 `(.)i/flow/login/page.tsx`으로 넘어감
  * 인터셉팅 라우터이면서 동시에 페러렐 라우터이기 때문에 `(beforeLogin)/layout.tsx`의 `{modal}` 에 그려지게 됨


> 💡 가로채기 당한 `i/flow/login/page.tsx` 도 필요  
> -> **새로고침** 했을 때는 `i/flow/login/page.tsx`가 실행되기 때문 (브라우저를 통해 처음 실행되었을 때)
>   * **링크**를 통해 가로채기할때는 `(.)i`가 실행
>   * 원본과 가로채기가 꼭 내용이 동일할 필요는 없음

<br>

### redirect

[redirect](https://nextjs.org/docs/app/api-reference/functions/redirect)

앱 라우터에서 redirect가 추가되어 쉽게 리다이렉트 가능

```
redirect(path, type)
```

* 서버에서 redirect 시키는 것 -> 인터셉팅이 제대로 되지 않음
* 클라이언트에서 링크를 클릭해서 리다이렉트해야만 인터셉팅이 제대로 동작
* 클라이언트 리다이렉트로 바꿔줘야함
  * 그렇지만 결국 page.tsx는 서버 컴포넌트인것이 좋기 때문에 추후 다시 변경 예정 
* `router.push`는 추가, `router.replace`는 대체 (뒤로가기 이슈 해결에 도움)

<br><br>

## 태그

### Link

* a 태그는 페이지가 새로고침되면서 넘어감, Link 태그는 새로고침 x

### Image 

* 이미지를 import해서 가져다 쓸 수 있음 (png 등)
* Image 태그를 사용하면 이미지를 알아서 최적화

<br><br>

## css module 

global은 모든 곳에서 적용되는 공통 css, 특정 페이지나 레이아웃에서 사용될 것들은 module.css

css module의 역할은 브라우저 개발자 도구에서 보면 클래스명 뒤에 랜덤한 문자가 붙는데, 모듈별로 다르게 만들어서 클래스명이 동일하더라도 실제로는 다른 클래스가 되도록 함   
scss 도입해서 css module과 같이 쓰면 좋음 

<br><br>

## 참고 사이트 

> https://nextjs.org/docs/app
