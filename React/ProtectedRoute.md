# ProtectedRoute

## 개념

여러 페이지에서 동일한 로직이 겹칠 경우, 특히 페이지 이동에 관한 경우  
**ProtectedRoute** 컴포넌트를 활용해 처리할 수 있음

* 로그인 한 사용자만 유저 페이지로 이동할 수 있도록 인증 프로세스 처리 

<br><br>

## 예시

```tsx
const ProtectedRoute = ({
  user,
  redirectPath = '/landing',
  children,
}) => {
  if (!user) {
    return <Navigate to={redirectPath} replace />;
  }

  return children ? children : <Outlet />;
};
```


<br><br>

## 참고 사이트

> https://www.robinwieruch.de/react-router-private-routes/
