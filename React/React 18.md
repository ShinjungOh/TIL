# React 18

## Rendering API - Client React DOM API

`react-dom/client API`를 사용하면 클라이언트(브라우저에서)에서 React 컴포넌트를 렌더링할 수 있음  
일반적으로 앱의 최상위 수준에서 **React 트리를 초기화하기 위해** 사용   
프레임워크가 대신 호출해줄 수도 있음 (Ex. Next.js, Remix, Gatsby)   
대부분의 컴포넌트에서는 이를 import하거나 사용할 필요가 없음

### createRoot

브라우저 DOM 노드 안에 React 컴포넌트를 표시하는 루트를 생성할 수 있음 

```
const root = createRoot(domNode, options?)
```

```tsx
import { createRoot } from 'react-dom/client';

const root = createRoot(document.getElementById('root'));
root.render(<App />);
```

1. `createRoot`를 호출하면 브라우저 DOM 엘리먼트 안에 콘텐츠를 표시할 수 있는 React 루트를 생성
2. React는 domNode에 대한 루트를 생성하고 그 안에 있는 DOM을 관리 
3. 루트를 생성한 후에는 `root.render`를 호출해, 렌더링된 React 컴포넌트를 표시  

* React만으로 빌드된 앱에서는 일반적으로 루트 컴포넌트에 대한 `createRoot` 호출이 하나만 존재
  * 프레임워크를 사용하는 경우, 프레임워크가 이 호출을 대신 수행할 수도 있음 
  * 필요한 경우, 루트를 필요한 만큼 많이 작성할 수도 있음
* createRoot는 `render`와 `unmount` 두 가지 메소드가 있는 객체를 반환

#### 주의점

* ⚠️ 앱이 `서버`에서 렌더링되는 경우 `createRoot` 사용 불가 -> `hydrateRoot` 사용할 것 
* 컴포넌트의 자식이 아닌 DOM 트리의 다른 부분(Ex. 모달 또는 툴팁)에 JSX 조각을 렌더링하려는 경우, createRoot 대신 `createPortal` 사용

#### `root.render(reactNode)`

`root.render`를 호출하여 JSX 조각(React 노드)을 React 루트의 브라우저 DOM 노드에 **표시**    
React는 root에 `<App />`을 표시하고 그 안에 있는 DOM을 관리

```tsx
root.render(<App />);
```

* reactNode : `createElement`로 작성한 React 엘리먼트, 문자열, 숫자, null, undefined 등
* root.render는 `undefined`를 반환

#### `root.unmount()`

React 루트 내부에서 렌더링된 트리를 **삭제**  
React만으로 작성된 앱에는 일반적으로 root.unmount에 대한 호출이 없음 

```tsx
root.unmount();
```

* `root.unmount`를 호출하면 루트에 있는 모든 컴포넌트가 unmount되고, 트리상의 이벤트 핸들러나 state가 제거되며, 루트 DOM 노드에서 React가 **분리**  
* `root.unmount`를 호출한 후에는 같은 루트에서 `root.render`를 재호출할 수 없음 
  * unmount된 루트에서 `root.render`를 호출하려고 하면 오류가 발생
  * 해당 노드의 이전 루트가 unmount된 후, 동일한 DOM 노드에 새로운 루트를 만들 수는 있음 
* root.unmount는 `undefined`를 반환

<br><br>

### hydrateRoot

이전에 `react-dom/server`에서 생성한 HTML 콘텐츠가 있는 브라우저 DOM 노드 안에 React 컴포넌트를 표시할 수 있음  
앱의 HTML을 `react-dom/server`로 생성했다면, 클라이언트에서 hydrate해주어야 함 

```
const root = hydrateRoot(domNode, reactNode, options?)
```

* domNode : 서버에서 루트 엘리먼트로 렌더링된 DOM element
* reactNode : 앞서 존재하는 HTML에 렌더링하기 위한 React 노드, `<App />` 같은 JSX 조각

```tsx
import { hydrateRoot } from 'react-dom/client';

hydrateRoot(document.getElementById('root'), <App />);
```

`hydrateRoot`를 호출하여 **서버 환경**에서 React가 이미 만들어둔 HTML에 React(컴포넌트의 로직)를 **붙임**

1. 서버 HTML을 브라우저 DOM 노드에서 React 컴포넌트를 이용해 hydrate 해줌  
2. Hydration을 거치면 서버에서 만들어진 초기 HTML 스냅샷이 브라우저에서 완전히 인터랙티브한 앱으로 전환 

> 💡 서버 렌더링은 HTML 스냅샷을 보여줌으로써 앱의 로딩이 더 빠르게 느껴지도록 함 

* React는 domNode 내부에 있는 HTML에 붙어서 그 내부의 DOM을 직접 관리   
* React만으로 만든 App에서는 보통 단일 루트 컴포넌트에 대해 `hydrateRoot`를 단 한 번만 호출
  * 프레임워크를 사용하는 경우, 프레임워크가 이 호출을 대신 수행할 수도 있음

#### 주의점

* ⚠️ hydrateRoot는 서버에서 렌더링된 내용과, 후에 렌더링된 내용이 동일할 것을 기대
  * -> 동일하지 않은 부분들은 버그로 인식하며, 직접 고쳐줘야 함  
* 개발 환경에서는 React가 hydration 중에 동일하지 않은 부분에 대해 경고
  * 속성이 동일하지 않을 경우, 해당 속성이 올바르게 적용될 것이라고 보장할 수 없음
  * 마크업이 동일하지 않는 경우는 드물고, 모든 마크업을 검증하는 비용은 굉장히 비싸므로, 이 동작은 성능상 중요
* App이 미리 렌더링된 HTML 없이 `클라이언트`에서만 렌더링하는 경우에는 `hydrateRoot`를 쓸 수 없음 -> `createRoot`를 사용

#### `root.render(reactNode)`

`hydrate`된 React 루트부터 내부 컴포넌트를 새로운 React 컴포넌트로 **갱신**하려면 `root.render`를 호출      
브라우저 DOM 요소들도 함께 갱신

```tsx
root.render(<App />);
```

React는 hydrate된 root부터 내부를 `<App />`으로 갱신

#### `root.unmount()`

root.unmount를 호출해 React 루트부터 그 하위에 렌더링된 트리를 삭제 

<br><br>

## Rendering API - Server React DOM API

서버에서 React 컴포넌트를 생성하는 API에 변경 - API 추가

### renderToPipeableStream

React 트리를 파이프 가능한 [Node.js 스트림](https://nodejs.org/api/stream.html)으로 렌더링

리액트 컴포넌트를 HTML로 렌더링하는 메소드, 스트림을 지원  
스트림을 사용하면 HTML을 점진적으로 렌더링하고 클라이언트에서는 중간에 script 삽입 가능  

`hydrateRoot`와 함께 사용하면, 서버에서 렌더링된 HTML을 클라이언트에서 hydration 가능  
-> 첫번째 로딩을 매우 빠르게 수행 

최초에 브라우저는 아직 불러오지 못한 데이터 부분을 Suspense의 fallback으로 받음  
💡 순서나 오래 걸리는 렌더링에 영향받지 않고 빠르게 렌더링 가능

<br>

### renderToReadableStream

`renderToPipeableStream`이 Node.js 환경에서의 렌더링을 위해 사용되는 반면,  
`renderToReadableStream`은 **웹 스트림**을 기반으로 작동

[Readable Web Stream](https://developer.mozilla.org/ko/docs/Web/API/ReadableStream)를 이용해 React tree를 그림 

* 서버 환경이 아닌 Cloudflare, Deno 같은 웹 스트림을 이용하는 환경에서 사용 가능
  * 모던 엣지 런타임 환경에서 사용  
* 웹 애플리케이션을 개발하는 경우에는 이 메서드를 사용할 일이 거의 없을 것

<br>

### renderToNodeStream 지원 중단 

renderToPipeableStream을 사용할 것을 권장 

<br><br>

## Automatic Batching(자동 배치)

React가 렌더링을 **자동으로 배치**함   
여러 상태 업데이트를 하나의 리렌더링으로 묶어서 성능을 향상시키는 방법

* 리액트 17이하의 버전에서는 이벤트 핸들러 내부에서는 자동 배칭이 이뤄졌지만,   
Promise, setTimeout 등의 비동기 작업은 자동 배칭이 이뤄지지 않았음  

-> 동기와 비동기 배치 작업에 일관성이 X   

=> 리액트 18버전부터는 루트 컴포넌트를 createRoot로 만들면 모든 업데이트가 배치 작업으로 최적화  

### createRoot

* createRoot를 사용하면 자동 배치가 활성화됨
* 동기, 비동기, 이벤트 핸들러 등에 상관 없이 렌더링을 배치 작업으로 처리

<br><br>

## Strict Mode 강화 

### 엄격 모드 개념 

```tsx
root.render((
    <React.StrictMode>
      <App />
    </React.StrictMode>
));
```

* `<App />` 컴포넌트 각각의 자손까지 검사가 이루어짐
* 개발자 모드에서만 작동

⚠️ Ex. useEffect 등을 사용할 때 콘솔에 두 번씩 호출하는 경우  
두 번 체크해서 두 결과가 다를 경우 함수의 사이드이펙트가 크다고 경고   
=> 함수형 프로그래밍 원칙에 따라 모든 컴포넌트는 항상 순수하다고 가정,  
순수한 결과를을 내고 있는지 확인시켜주기 위해 두 번 실행 

<br>

### 1. UNSAFE_가 붙은 생명주기 메소드 사용 시 경고

### 2. 문자열 ref 사용 시 경고

* 여러 컴포넌트에 걸쳐 사용될 수 있음 -> 충돌 우려
* 실제 어떤 ref애서 참조되고 있는지 파악하기 어려움

### 3. findDOMNode 사용 시 경고

* 클래스형 컴포넌트 인스턴스에서 실제 DOM 요소에 대한 참조를 가져올 수 있는 메소드
* 현재는 사용이 권장되지 않음
* 문자열 ref와 마찬가지로, createRef나 useRef를 사용하는 것이 좋음

### 4. 레거시 context API 사용 시 경고

* childContextTypes, getChildContext 등을 사용하는 경우

<br><br>

## New Hooks

### useId

> Other Hooks

접근성 속성에 전달할 수 있는 고유 ID를 생성하기 위한 React Hook  
ID를 하드코딩하는 대신, `useId`로 고유한 ID를 생성해서 사용할 수 있음 

```ts
const id = useId();
```

* ⚠️ useId 목록에 키를 생성하는 것이 아니며, 키는 데이터에서 생성해야 함
* 새로운 스트리밍 서버 렌더러가 HTML을 잘못된 순서로 전달하는 방식 때문에 React 18에서는 더욱 중요

<br>

### useTransition

> Performance Hooks

UI를 차단하지 않고 state를 업데이트할 수 있는 React Hook

일부 상태 업데이트를 **긴급하지 않은 것으로 표시**할 수 있음  
기타 상태 업데이트는 기본적으로 긴급 업데이트로 간주됨 

```ts
const [isPending, startTransition] = useTransition();
```

* 컴포넌트의 최상위 레벨에서 `useTransition`을 호출해, 일부 state 업데이트를 트랜지션으로 표시

<br>

### useDeferredValue

> Performance Hooks

UI 일부의 업데이트를 지연시킬 수 있는 React Hook  

트리에서 긴급하지 않은 부분의 리렌더링을 연기할 수 있음    
디바운싱과 유사하지만 추가적인 장점이 존재 

* 고정된 시간 지연이 없음 -> React는 첫 번째 렌더링이 화면에 반영된 직후, 지연된 렌더링을 시도 
* 지연된 렌더링은 중단 가능하며, 사용자 입력을 차단하지 않음 

```ts
const deferredValue = useDeferredValue(value);
```

<br>

### useSyncExternalStore

> Other Hooks

외부 스토어를 구독할 수 있는 React Hook 

저장소에 대한 업데이트를 **동기식으로 강제**하여, 외부 저장소가 동시 읽기를 지원할 수 있도록 함   
외부 데이터 소스에 대한 구독을 구현할 때 `useEffect`가 필요하지 않음  
React 외부 상태와 통합되는 모든 라이브러리에 권장됨 

```ts
const snapshot = useSyncExternalStore(subscribe, getSnapshot, getServerSnapshot?);
```

* 애플리케이션 코드가 아닌 `라이브러리에서` 사용하도록 고안된 훅
* 컴포넌트의 최상위 레벨에서 useSyncExternalStore를 호출하여 외부 데이터 저장소에서 값을 읽음 

<br>

### useInsertionEffect

> Effect Hooks

CSS-in-JS 라이브러리가 렌더링에 스타일을 주입하는 성능 문제를 해결할 수 있게 해주는 Hook

`useEffect`의 버전 중 하나로, DOM 변이 전에 실행됨

```ts
useInsertionEffect(setup, dependencies?);
```

* 애플리케이션 코드가 아닌 `라이브러리에서` 사용하도록 고안된 훅 
* Effect는 **클라이언트**에서만 실행되며, 서버 렌더링 중에는 실행되지 않음 
* 내부에서는 state를 업데이트할 수 없음 
* `useInsertionEffect`가 실행될 때까지는 refs가 아직 첨부되지 않았고, DOM이 아직 업데이트되지 않았음 

<br><br>

## 참고 사이트

> https://react.dev/blog/2022/03/08/react-18-upgrade-guide  
> https://react.dev/blog/2022/03/29/react-v18   
> https://react-ko.dev/reference/react-dom/client  
> https://ko.react.dev/reference/react-dom/server
