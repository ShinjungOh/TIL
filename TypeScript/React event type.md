# React event type

## ChangeEvent

React에서 제공하는 **제네릭 타입** 중 하나    
HTML input 요소의 값이 변경될 때 발생하는 이벤트를 나타냄

* **React에서 기본적으로 제공**되기 때문에 일반적으로 React 컴포넌트에서 사용할 때 오류가 발생하지 않음
    * React의 이벤트 핸들러에서 ChangeEvent를 사용할 때는 일반적으로 제대로 동작하며, 타입이 제대로 추론됨
    * ChangeEvent를 사용해 함수의 매개변수 e를 타입 지정하는 것은 일반적인 패턴

<br><br>

## KeyboardEvent, MouseEvent

React에서 제공하는 **제네릭 타입** 중 하나

* KeyboardEvent와 MouseEvent는 **DOM 이벤트 객체**를 나타냄    
  * -> 이벤트 타입은 DOM에서 제공하는 것을 그대로 사용해야 함   
  * -> 이 이벤트 타입을 사용할 때는 React의 제네릭 버전을 사용해야 함

```tsx
import { KeyboardEvent, MouseEvent } from 'react';
```

<br><br>

## 오류 메시지

```
src/pages/SigninPage.tsx:75:32 - error TS2315: Type 'KeyboardEvent' is not generic.
75   const handleOnKeyPress = (e: KeyboardEvent<HTMLInputElement>) => {
                                  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
                                  
src/pages/SigninPage.tsx:81:38 - error TS2315: Type ‘MouseEvent’ is not generic.
81   const handleChangePageSignup = (e: MouseEvent<HTMLAnchorElement>) => {
                                        ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```

### 해결 방법

자동완성으로 import되지 않는 경우도 있기 때문에 직접 { } 안에 추가하면 됨 

```
import { KeyboardEvent, MouseEvent, ChangeEvent, useEffect } from 'react';
```

<br><br>

## index.d.ts

```ts
// ChangeEvent
interface ChangeEvent<T = Element> extends SyntheticEvent<T> {
    target: EventTarget & T;
}

interface SyntheticEvent<T = Element, E = Event> extends BaseSyntheticEvent<E, EventTarget & T, EventTarget> {
}
```

* React에서 제공하는 SyntheticEvent를 기반으로 하고 있으며, 기본적으로 Element를 대상으로 함
* ChangeEvent의 target 속성은 EventTarget & T 유형
  * -> ChangeEvent가 어떤 요소에 대한 이벤트인지를 나타내며, 기본적으로 Element로 설정


<br>

```ts
// KeyboardEvent 
interface KeyboardEvent<T = Element> extends UIEvent<T, NativeKeyboardEvent> {
    // ... 
}

// MouseEvent
interface MouseEvent<T = Element, E = NativeMouseEvent> extends UIEvent<T, E> {
    // ...
}

interface UIEvent<T = Element, E = NativeUIEvent> extends SyntheticEvent<T, E> {
}
```

* KeyboardEvent와 MouseEvent는 UIEvent를 기반으로 하고 있음
* T 매개변수를 사용하여 이벤트 대상의 유형을 지정
  * -> 이벤트가 어떤 요소에 대한 것인지를 나타내며, 기본적으로 Element로 설정
