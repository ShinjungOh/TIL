# Next.js

## Next.js concept

> https://nextjs.org/docs

React 기반의 프레임워크
* 폴더 및 파일 기반으로 라우팅 지원
* 서버 사이드 렌더링 지원
  * **SSR** : 서버에서 페이지를 그려 클라이언트(브라우저)로 보낸 후 화면에 표시하는 기법
* SEO 적용 수월
* 스태틱 파일 지원

<br><br>

## 사용방법
### 설치
> npx create-next-app --typescript

<br>

### 실행 
> npm run dev

<br><br>

## 라우팅
pages 폴더 안에 각 page를 만들면, 별도의 작업 없이 라우팅이 적용

### 다이나믹 라우팅 
* pages 아래에 하위 폴더 생성
* 대괄호를 이용해 파일명 생성 
  * <em> Ex) [id].js </em>

<br><br>

## 레이아웃
### 1️⃣ _app.js
레이아웃을 만들기 위해서는 **_app.js** 파일을 이용 <br>
모든 페이지는 **_app.js**를 통한다.
* 페이지 전환 시 레이아웃 유지
* 페이지 전환 시 상태값 유지
* componentDidCatch를 이용해 커스텀 에러 핸들링 가능
* 추가적인 데이터를 페이지로 주입 가능
* export default 하단에 글로벌 CSS 작성

<br>

```javascript
function MyApp({ Component, pageProps }) {
    
}
```

#### Component
props로 넘어온 Component는 현재 페이지를 의미   
페이지 전환 시, Component props가 변경됨 

<br>

### 2️⃣ 컴포넌트 만들기 
컴포넌트 생성 후, **_app.js**에서 불러온다.

Project/src/component/Header.js
Project/src/component/Footer.js

```javascript
import Header from "경로";
import Footer from "경로";

function MyApp({ Component, pageProps }) {
    return
    <div>
        <Header />
        <Component {...pageProps} />
        <Footer />
    </div>
}
```

<br>

### 3️⃣ public 폴더
스태틱(정적) 파일 제공
* HTML 파일
* robots 파일
* 이미지 
  * /images/logo.png 같은 방법으로 호출
  
<br>

### 4️⃣ _document.js
> https://nextjs.org/docs/advanced-features/custom-document

Next.js에서 제공하는 document를 커스터마이징 가능 <br> 

```javascript
import { Html, Head, Main, NextScript } from 'next/document'

export default function Document() {
  return (
    <Html lang="ko">
      <Head />
      <body>
        <Main />
        <NextScript />
      </body>
    </Html>
  )
}
```

Next.js는 마크업 정의를 건너뛰기 때문에, Html, Head, body를 수정하려면 **_document.js**를 필수적으로 사용해야 함

* 서버에서만 렌더링
* 이벤트 핸들러 작동 x
* CSS 사용 x
* 모든 페이지에 적용되어야 하는 내용은 **_app.js**에서 처리
* _app.js, _document.js에서 사용하는 Head는 다름
