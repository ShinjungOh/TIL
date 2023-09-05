# PropsWithChildren

## React 18

* React.FC 타입에서 암묵적인 children 선언 제거
* PropsWithChildren 타입 추가

<br><br>

## PropsWithChildren

children을 포함한 props를 가리키는 타입

```
type PropsWithChildren<P = unknown> = P & { children?: ReactNode | undefined };
```

<br>

### 사용방법 

```tsx
type ComponentProps = {
    someProperty: string;
};

function Component({someProperty, children}: PropsWithChildren<ComponentProps>) {
    // ...
}
```


```tsx
type Props = {
    title?: string;
};

const Component: React.FC<React.PropsWithChildren<Props>> = ({children}) => {
    // ...
}
```

<br>

### 예시

```tsx
import React, {PropsWithChildren} from 'react';

type OverlayProps = {
    onClose: () => void;
    onClickOverlayClose: boolean;
};

type Props = PropsWithChildren<OverlayProps>;

export default function Overlay({onClose, onClickOverlayClose, children}: Props) {
    // ...
}
```

<br><br>

## 참고 사이트

> https://ko.legacy.reactjs.org/versions/  
> https://blog.shiren.dev/2022-04-28/    
> https://dev.to/maafaishal/unsafe-propswithchildren-utility-type-in-react-typescript-app-3bd3
