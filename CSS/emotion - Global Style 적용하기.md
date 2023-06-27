# Emotion

## Global Style

### 1. `GlobalStyle.tsx` 파일 생성

* import 주의
* 하단에 Global 컴포넌트 사용 주의 

```tsx
import { css, Global } from '@emotion/react';

const style = css`
  html {
    box-sizing: border-box;
  }

  *,
  *::before,
  *::after {
    box-sizing: inherit;
    background-color: #646cff;
  }

  html {
    font-size: 62.5%;
  }

  body {
    font-size: 1.6rem;
    background: ${(props) => props.theme.colors.background};
    color: ${(props) => props.theme.colors.text};
  }

  :lang(ko) {
    h1,
    h2,
    h3 {
      word-break: keep-all;
    }
  }
`;

const GlobalStyle = () => {
  <Global styles={style} />;
};

export default GlobalStyle;
```

<br>

### 2. `App.tsx`에 GlobalStyle 적용 

```tsx
import GlobalStyle from './styles/GlobalStyle';

export default function App() {
  return (
    <Page>
      <GlobalStyle />
      <RouterProvider router={router} />
    </Page>
  );
}
```
