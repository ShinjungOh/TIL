# index로 모듈화하기

## index.ts 파일 생성하기

각 디렉토리별로 하나의 index 파일을 생성

```
│  ├─ pages
│  │   ├─ AuthKakaoPage.tsx
│  │   ├─ CalendarPage.tsx
│  │   ├─ EditPostPage.tsx
│  │   ├─ HomePage.tsx
│  │   ├─ ProtectedRoute.tsx
│  │   ├─ ReportPage.tsx
│  │   ├─ SettingPage.tsx
│  │   ├─ SigninPage.tsx
│  │   ├─ SignupPage.tsx
│  │   ├─ TimelinePage.tsx
│  │   ├─ WritePostPage.tsx
│  │   └─ index.ts ✅
```

<br><br>

## index.ts 파일 작성하기

전체 선택자 * 를 사용해 각 파일의 export가 붙은 요소 내보내기   
⚠️ export default로 내보냈던 요소가 있다면 default를 삭제

```ts
export * from './AuthKakaoPage';
export * from './CalendarPage';
export * from './EditPostPage';
export * from './HomePage';
export * from './ProtectedRoute';
export * from './ReportPage';
export * from './SigninPage';
export * from './SignupPage';
export * from './SettingPage';
export * from './TimelinePage';
export * from './WritePostPage';
```

```tsx
// 기존
export default function CalendarPage() {
  // ...
}


// 수정 후 ✅
export function CalendarPage() { 
  // ...
}
```

<br><br>

## 결과

### 기존

```tsx
import RouterLayout from './ui/components/RouterLayout';
import HomePage from './pages/HomePage';
import SigninPage from './pages/SigninPage';
import SignupPage from './pages/SignupPage';
import ProtectedRoute from './pages/ProtectedRoute';
import CalendarPage from './pages/CalendarPage';
import TimelinePage from './pages/TimelinePage';
import ReportPage from './pages/ReportPage';
import SettingPage from './pages/SettingPage';
import AuthKakaoPage from './pages/AuthKakaoPage';
import WritePostPage from './pages/WritePostPage';
import EditPostPage from './pages/EditPostPage';
```

### 모듈화 적용 후 

```tsx
import {
  AuthKakaoPage,
  CalendarPage,
  EditPostPage,
  HomePage,
  ProtectedRoute,
  ReportPage,
  SettingPage,
  SigninPage,
  SignupPage,
  TimelinePage,
  WritePostPage,
} from './pages';
```

<br><br>

## 테스트 오류

> index에서 `export * from './파일명'`으로 내보냈을 때 테스트에서 오류가 발생하는 경우 

이 파일을 사용하는 곳에서 미처 다 import 해오기 전에,
테스트 코드가 이미 실행이 되어버려서 문제가 발생  

### default로 내보내기  

```ts
// globalStyle.css.ts
export default globalStyle;

// styleToken.css.ts
export default styleToken;
```

### index.ts

```ts
// index.ts
export { default as globalStyle } from './globalStyle.css';
export { default as styleToken } from './styleToken.css';
```
