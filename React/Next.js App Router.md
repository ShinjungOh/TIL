# Next.js

## App Router

## Routing

페이지에 관한 것은 app 디렉토리의 하위에 생성  
import의 @ 는 src를 나타냄

### 디렉토리 이름

* (소괄호) : 주소창에 관여하지 않음, 그룹을 만들 수 있음, 레이아웃
* [대괄호] : 다이나믹 라우팅, 슬러그(slug)

### layout.js

[layout.js](https://nextjs.org/docs/app/api-reference/file-conventions/layout)

경로 간에 공유되는 UI

* 레이아웃, 페이지는 함수 이름이 중요하지 않음, export default만 해주면 됨

### page.js

[page.js](https://nextjs.org/docs/app/api-reference/file-conventions/page)

페이지는 경로에 고유한 UI

* 레이아웃, 페이지는 함수 이름이 중요하지 않음, export default만 해주면 됨

### template.js

[template.js](https://nextjs.org/docs/app/api-reference/file-conventions/template)

페이지 넘길 때 레이아웃도 리렌더링 되게 하고 싶으면 template.tsx 사용

* layout: 리렌더링 x
* template:  리렌더링 ㅇ
  * 페이지 넘길때마다 무언가를 기록해야할 때 (GA 등)
* 둘이 공존하면 안됨

### Parallel Routes

[Parallel Routes](https://nextjs.org/docs/app/building-your-application/routing/parallel-routes)

뒤 페이지 그대로 두고 모달 띄우는 방법  
같은 폴더에 있어야 작동하며, 레이아웃에서 사용 가능  
**두가지 화면을 한 페이지에서 보여줄 수 있음**

* @ 뒤의 이름(Ex. modal)이 레이아웃의 props가 됨
* @ 아래로 경로 맞추어야 함
* @ 는 주소에 해당하지 않음 

#### default.tsx

패러렐 라우트에 대한 기본값, 패러렐 라우트가 필요 없을 때  
⚠️ 없으면 오류 발생  

```tsx
// 주소가 z.com (localhost:3000) 일 때

return (
    // ... 
    {children} // children -> page.tsx
    {modal} // modal -> @modal/default.tsx
)
```

패러렐 라우트에서 모달을 2개 이상 띄우고 싶으면 `@modal2` 등의 폴더 생성, `default.tsx` 생성


### 인터셉트 라우트




### 태그 

* a 태그는 페이지가 새로고침되면서 넘어감, Link 태그는 새로고침 x 
* 이미지를 import해서 가져다 쓸 수 있음 (png 등)
* Image 태그를 사용하면 이미지를 알아서 최적화

### redirect

[redirect](https://nextjs.org/docs/app/api-reference/functions/redirect)

앱 라우터에서 redirect가 추가되어 쉽게 리다이렉트 가능

```
redirect(path, type)
```

* 서버에서 redirect 시키는 것 -> 인터셉팅이 제대로 되지 않음
* 클라이언트에서 링크를 클릭해서 리다이렉트해야만 인터셉팅이 제대로 동작
* 클라이언트 리다이렉트로 바꿔줘야함
  * 그렇지만 결국 page.tsx는 서버 컴포넌트인것이 좋아서 추후 다시 변경
* router.push는 추가, router.replace는 대체 (뒤로가기 이슈 해결에 도움)

### css module 

global은 모든 곳에서 적용되는 공통 css, 특정 페이지나 레이아웃에서 사용될 것들은 module.css

<br><br>

## 참고 사이트 

> https://nextjs.org/docs/app
