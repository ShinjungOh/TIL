# React Router

## 뒤로가기 방지

로그인을 해야 접근할 수 있는 페이지의 경우, 로그아웃을 해서 유저 토큰 값이 없을 때 사용

<br><br>

## replace 사용법

`replace: true`

```js
import { useNavigate } from 'react-router';

const navigate = useNavigate();

const onClickLogout = () => {
    navigate('/',  { replace: true });
}
```

navigate의 url로 넘어간 후에는 뒤로가기를 하더라도 이전 페이지로 돌아올 수 없음   
