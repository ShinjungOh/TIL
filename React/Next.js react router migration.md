# Migrating from React Router

## 프로젝트 생성

`yarn create react-app react-router-origin --template react-router-dom`  
`yarn create react-app react-router-next --template react-router-dom`

<br><br>

## package.json

1️⃣ react-router-dom 제거  
`yarn remove react-router-dom`

<br>

2️⃣ react-scripts 제거  
`yarn remove react-scripts`

<br>

3️⃣ next 설치  
`yarn add next`

<br>

4️⃣ package.json script 수정
```json
"scripts": {
"dev": "next dev",
"build": "next build",
"start": "next start"
},
```

<br>

5️⃣ .gitignore에 .next 추가
```
# dependencies
/node_modules
/.pnp
.pnp.js
.next
```

<br><br>

## 프로젝트 구조, 파일 변경
* `import link from 'react-router-dom'` -> `import Link from 'next/link'`로 교체
* App.test.js 제거
* App.js 내 Router 로직 -> pages 폴더 구조로 대체
* _document.js, _app.js, style, Image 적용
* scroll restoration 도 next/link와 next/router 사용하면 기본 제공

<br><br>

## 참고 사이트

> https://nextjs.org/docs/migrating/from-react-router  
> https://nextjs.org/docs/advanced-features/custom-document  
> https://nextjs.org/docs/advanced-features/custom-app  
