# React 18


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
