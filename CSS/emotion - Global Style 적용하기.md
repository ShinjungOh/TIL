# Emotion

## Global Style

### 1. `globalStyle.css.ts` 파일 생성

* import 주의

```ts
import { css } from '@emotion/react';

const globalStyle = css`
  html {
    box-sizing: border-box;
  }

  html, body, div, span, applet, object, iframe,
  h1, h2, h3, h4, h5, h6, p, blockquote, pre,
  a, abbr, acronym, address, big, cite, code,
  del, dfn, em, img, ins, kbd, q, s, samp,
  small, strike, strong, sub, sup, tt, var,
  b, u, i, center,
  dl, dt, dd, ol, ul, li,
  fieldset, form, label, legend,
  table, caption, tbody, tfoot, thead, tr, th, td,
  article, aside, canvas, details, embed, 
  figure, figcaption, footer, header, hgroup, 
  menu, nav, output, ruby, section, summary,
  time, mark, audio, video {
    margin: 0;
    padding: 0;
    border: 0;
    font: inherit;
    vertical-align: baseline;
  }

  /* HTML5 display-role reset for older browsers */

  article,
  aside,
  details,
  figcaption,
  figure,
  footer,
  header,
  hgroup,
  menu,
  nav,
  section {
    display: block;
  }

  ol,
  ul {
    list-style: none;
  }

  blockquote,
  q {
    quotes: none;
  }

  blockquote:before,
  blockquote:after,
  q:before,
  q:after {
    content: none;
  }

  table {
    border-collapse: collapse;
    border-spacing: 0;
  }

  *,
  *::before,
  *::after {
    box-sizing: inherit;
  }

  html {
    font-size: 62.5%;
  }

  body {
    font-size: 1.6rem;
    line-height: 1;
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

export default globalStyle;
```

<br>

### 2. `App.tsx`에 GlobalStyle 적용 

* Global 컴포넌트 사용 주의

```tsx
import { Global } from '@emotion/react';
import globalStyle from './styles/globalStyle.css';

export default function App() {
  return (
    <Page>
        <RouterProvider router={router} />
        <Global styles={globalStyle} />
    </Page>
  );
}
```

<br><br>

## 참고 사이트 

> https://emotion.sh/docs/globals  
> [Next.js에 Emotion 적용하기](https://velog.io/@s_sangs/Next.js%EC%97%90-Emotion-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0)  
> [styled-components를 emotion으로 변환하기](https://velog.io/@godud2604/styled-components-%EB%A5%BC-emotion-%EC%9C%BC%EB%A1%9C-%EB%B3%80%ED%99%98%ED%95%98%EA%B8%B0)
