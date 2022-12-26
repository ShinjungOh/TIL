# const 폴더로 자주 사용하는 값 관리하기

## constant 

자주 사용하는 값을 모아 const 폴더 안에서 파일로 관리

### 장점

* 수정, 삭제 용이
* 값이 바뀌었을 때 일일이 찾아다니며 바꿔주지 않아도 됨
* 재활용 가능

<br><br>

## 폴더 구조

> 📦 src  
┣ 📁lib  
┃ ┣ 📁 const  
┃ ┃ ┗ 📄 path.ts

<br><br>

## 예시

```js
// src/lib/const/path.ts

export const PATH = {
  HOME: '/',
  SIGN_IN: '/signin',
  SIGN_UP: '/signup',
  COMPONENT: '/component',
};
```

```js
// src/Router.tsx

import { Route, Routes } from 'react-router-dom';
import React from 'react';

import { PATH } from './lib/const/path';
import {
  SignInPage, SignUpPage, Component, Home,
} from './ui/pages';

const Router = () => (
  <Routes>
    <Route path={PATH.HOME} element={<Home />} />
    <Route path={PATH.SIGN_IN} element={<SignInPage />} />
    <Route path={PATH.SIGN_UP} element={<SignUpPage />} />
    <Route path={PATH.COMPONENT} element={<Component />} />
  </Routes>
);

export default Router;
```

* 라우터 주소가 바뀌어도 const 폴더의 path.ts 파일에서 교체해주면 됨 
  * 라우터와 페이지 컴포넌트에서 이동하는 url이 다 바뀌어서 효율적으로 구성 가능
