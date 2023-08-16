# CSS-in-JS 

## 라이브러리

styled-components, emotion

React 컴포넌트의 상태나 속성을 동적으로 스타일링에 적용할 수 있음

<br><br>

## 문법

### `${(props) => ...}` 

컴포넌트의 props를 스타일 내에서 활용  
템플릿 리터럴을 이용해서 함수를 사용하는 문법    
props를 이용해서 컴포넌트의 속성을 읽고, 스타일을 동적으로 조정할 수 있음

### 주의점

```tsx
const FeelingCatImage = styled.img<{ isSelected: boolean }>`
  width: 100%;
  height: 100%;
  opacity: ${(props) => (props.isSelected ? '100%' : '45%')};
`;
```

```tsx
opacity: ${(isSelected) => (isSelected ? '100%' : '45%')};  // ❌ 
opacity: ${(props) => (props.isSelected ? '100%' : '45%')}; // ✅
``` 

isSelected를 직접 사용하면 문법적으로는 문제가 없을 수 있지만,  
isSelected가 **JSX 컴포넌트의 속성**이므로 정상적으로 작동하지 않을 수 있음 

이 문법은 일반적인 자바스크립트 문법이지만, JSX 내에서는 이런 방식으로 동작하지 않는 경우가 많음  
CSS-in-JS 라이브러리를 사용할 때는 템플릿 리터럴 내에서 **props**를 사용하는 방식을 이용해야 함
