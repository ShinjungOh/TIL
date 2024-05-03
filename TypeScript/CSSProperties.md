# TypeScript

## CSSProperties

CSS 스타일 속성을 나타내는 객체의 타입을 지정할 때 사용
react 패키지에서 제공하는 타입

* React에서 인라인 스타일을 사용할 때 `CSSProperties`를 사용해 style prop으로 전달된 객체를 설명할 수 있음
* `CSSProperties` 타입은 가능한 모든 CSS 프로퍼티의 집합
* 유효한 CSS 속성을 style prop에 전달하고 에디터에서 자동 완성을 얻을 수 있음

```ts
interface MyComponentProps {
  style: React.CSSProperties;
}
```

<br><br>

## 예시

```tsx
import { CSSProperties } from 'react';

const customStyle: CSSProperties = {
  color: 'red',
  fontSize: '16px',
  fontWeight: 'bold',
};
```

* React 컴포넌트에서 style 속성을 사용해 인라인 CSS를 지정할 때 활용 
* customStyle 객체는 color, fontSize, fontWeight 등의 CSS 속성을 가질 수 있음
  * 속성들은 모두 string 값이어야 함 
* CSSProperties는 TypeScript에서 정적 타입 검사를 수행하기 위해 사용됨
  * -> 잘못된 CSS 속성이나 값이 사용될 때 컴파일러가 경고를 표시

<br><br>

## 참고 사이트

> https://react-ko.dev/learn/typescript#typing-style-props

