# React Router

## 동적 라우팅

라우트 경로에 특정 값을 넣어 해당하는 페이지로 이동할 수 있게 하는 것  
웹사이트의 상세 페이지 구현에 사용 

<br><br>

## 사용 방법

### 1️⃣ Route의 path 안에 '/category/:id' 형태의 경로 추가 

```js
import { Route, Routes } from 'react-router-dom';
import React from 'react';

const Router = () => (
  <Routes>
    <Route path={PATH.HOME} element={<Home />} />
    <Route path={PATH.GUGUDAN} element={<GugudanPage />} />
  </Routes>
);
```

```js
// PATH를 따로 분리해 관리하는 경우

export const PATH = {
  HOME: '/',
  GUGUDAN: '/gugudan/:id',
};
```

* `Path Parameter` 경로 끝에 들어가는 각기 다른 id값을 저장하는 매개 변수
* `id` 해당 Path Parameter의 이름, 임의로 이름을 지정할 수 있음
* `:` Path Parameter가 올 것임을 의미, 동적 라우팅을 사용한다는 뜻

<br>

### 2️⃣ url에 담긴 id값 가져오기

`useParams` 
* react router에서 제공하는 함수, hook
* Path Parameter에 관한 정보를 담음

```js
import React from 'react';
import { useParams } from 'react-router';

const GugudanPage = () => {
  const params = useParams();
  const { id } = params;

  return (
    <>
      구구단 페이지 id: {id}
    </>
  );
};
```

<br><br>

## 참고 사이트

> https://reactrouter.com/en/main/hooks/use-params  
> https://velog.io/@zzangzzong/React-%EB%8F%99%EC%A0%81%EB%9D%BC%EC%9A%B0%ED%8C%85Dynamic-Routing
