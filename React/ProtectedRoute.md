# ProtectedRoute

## 개념

여러 페이지에서 동일한 로직이 겹칠 경우, 특히 페이지 이동에 관한 경우  
**ProtectedRoute** 컴포넌트를 활용해 처리할 수 있음    
고차 컴포넌트 방식 

* 로그인 한 사용자만 유저 페이지로 이동할 수 있도록 인증 프로세스 처리 

<br><br>

## 고차 컴포넌트 

고차 컴포넌트(HOC, Higher Order Component)  

컴포넌트 로직을 재사용하기 위한 React의 고급 기술  
고차 컴포넌트(HOC)는 React API의 일부가 아니며, React의 구성적 특성에서 나오는 패턴  

**고차 컴포넌트는 컴포넌트를 가져와 새 컴포넌트를 반환하는 함수**

```const EnhancedComponent = higherOrderComponent(WrappedComponent);```


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

```tsx
export default function ProtectedRoute({ children }: any) {
  const navigate = useNavigate();

  const isAccessToken = localStorage.getItem(ACCESS_TOKEN);
  if (!isAccessToken) {
    navigate(PATH.SIGN_IN);
  }

  return children;
}
```

<br><br>

## 참고 사이트

> https://www.robinwieruch.de/react-router-private-routes/  
> https://ko.legacy.reactjs.org/docs/higher-order-components.html
