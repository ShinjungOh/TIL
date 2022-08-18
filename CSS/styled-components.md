# Styled-components

## 사용법

```javascript
import React from 'react';
import styled from 'styled-components';

<Button>Styled Button</Button>

const Button = styled.button`

`;
```

<br><br>

## Styled component에 Props 전달하기

* 조건부 스타일링 가능

```javascript
<Button>Default yellow button</Button>
<Button color={"red"}>Custom red button</Button>

const Button = styled.button`
    background: ${props => props.color ? props.color : 'yellow'};
`;
```

<br><br>

## Styled component 상속받기

```javascript
<Button>Default Button</Button>
<RedButton>Red Button</RedButton>  // 상속 받아서 만든 버튼

const Button = styled.button`
    background-color: yellow;
    border: 1px solid red;
    color: green;
`;

// extends <Button />
const RedButton = styled(Button)`
    &:hover {
        background-color: red;
    }
`;
```

<br><br>

## 참고 사이트

> https://kimdabin.tistory.com/entry/Styled-Components-%EA%B0%84%EB%8B%A8-%EC%A0%95%EB%A6%AC-Basic  
> https://react.vlpt.us/styling/03-styled-components.html  
