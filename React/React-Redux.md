# React-Redux

## 프로젝트 생성

### 라이브러리 설치

```
yarn add redux react-redux
```

<br><br>

## 프로젝트 패턴

프레젠테이셔널 컴포넌트와 컨테이너 컴포넌트를 분리
* 프레젠테이셔널 컴포넌트 `src/components`
    * 주로 상태 관리가 이루어지지 않고, 그저 props를 받아 와서 화면에 UI를 보여 주기만 하는 컴포넌트
* 컨테이너 컴포넌트 `src/containers`
    * 리덕스와 연동되어 있는 컴포넌트
    * 리덕스로부터 상태를 받아 오거나, 리덕스 스토어에 액션을 디스패치
    

![](../Images/리액트_리덕스_패턴.png)


### 장점
* 코드의 재사용성 증가
* 관심사의 분리 -> UI를 작성할 때 편리

<br>

## 리덕스 구조

### 1. 각각 다른 파일에 작성

가장 기본적이지만 불편할 수 있음

```md
├── actions
│   ├── counter.js
│   └── todos.js
├── constants
│   └── ActionTypes.js
└── reducers
    ├── counter.js
    └── todos.js
```

### 2. 기능별로 묶어 파일 하나에 작성 ✅

Ducks 패턴   
액션 타입, 액션 생성 함수, 리듀서 함수를 기능별로 파일 하나(**모듈**)에 몰아서 작성하는 방식

```md
└── modules
    ├── counter.js
    └── todos.js
```

<br>

### 루트 리듀서

`createStore` 함수를 사용해 스토어를 만들 때는 리듀서를 하나만 사용해야 함  
이를 위해 기존의 리듀서들을 하나로 합치는 작업을 할 때, 리덕스의 `combineReducers` 함수를 사용

```js
import { combineReducers } from 'redux';
import counter from './counter';
import todos from './todos';

const rootReducer = combineReducers({
  counter,
  todos,
});

export default rootReducer;
```

<br>

### 스토어

컴포넌트에서 스토어를 사용할 수 있도록 react-redux에서 제공하는 **Provider** 컴포넌트로 App 컴포넌트를 감싸야 함      
props로는 store를 전달  


```js
import { createStore } from 'redux';
import rootReducer from './modules';
import { Provider } from 'react-redux';
import { composeWithDevTools } from 'redux-devtools-extension';

const store = createStore(rootReducer, composeWithDevTools()); // 스토어 생성, 루트 리듀서 전달

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
    <Provider store={store}>
      <App />
    </Provider>,
);
```

<br><br>

## 리덕스 개발자 도구

> `Redux DevTools`
> https://chrome.google.com/webstore/search/redux  

### 1. 패키지 없이 적용하기

```js
conststore = createStore(
    rootReducer, /* preloadedState,*/
    window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
);
```

### 2. 패키지 설치해서 적용하기 ✅  

```
yarn add redux-devtools-extension
```

```js
import { composeWithDevTools } from 'redux-devtools-extension';

const store = createStore(rootReducer, composeWithDevTools());
```

![](../Images/react-redux-devtools.png)

<br><br>

## redux-actions

```
yarn add redux-actions
```

* `createAction` 액션 생성 함수를 간단하게 선언
* `handleActions(각 액션에 대한 업데이트 함수, 초기 상태)`
  * 리듀서를 작성할 때 switch/case 문이 아닌 `handleActions` 함수를 사용해, 각 액션마다 업데이트 함수를 설정하는 형식으로 작성 가능    

<br>

### createAction

createAction으로 액션을 만들면 **액션에 필요한 추가 데이터**는 `payload` 라는 이름을 사용  

```js
const MY_ACTION = 'sample/MY_ACTION';
const myAction = createAction(MY_ACTION);
const action = myAction('hello world');

/*  결과:
    { type: MY_ACTION, payload: 'hello world' }
*/
```

액션 생성 함수에서 받아 온 **파라미터에 변형**을 줄 때, createAction의 두 번째 함수에 payload를 정의하는 함수를 따로 선언해서 넣으면 됨

```js
const MY_ACTION = 'sample/MY_ACTION';
const myAction = createAction(MY_ACTION,text=>`${text}!`);
const action = myAction('hello world');

/*  결과:
    { type: MY_ACTION, payload: 'hello world!' }
*/
```

<br>

### handleActions

액션 생성 함수는 액션에 필요한 추가 데이터를 모두 payload라는 이름으로 사용하기 때문에  
모두 공통적으로 `action.payload` 값을 조회하도록 리듀서를 구현해야 함   

```js
[CHANGE_INPUT]: (state, action) => ({ ...state, input: action.payload })
```

💡 객체 비구조화 할당으로 actions 값의 payload 이름을 새로 설정하면 정확한 action.payload 값을 알 수 있음

```js
[CHANGE_INPUT]: (state, { payload: input }) => ({ ...state, input })
```

<br><br>

## immer

리듀서에서 상태를 업데이트할 때는 불변성 유지를 위해 spread 연산자와 배열의 내장 함수를 활용     
-> 모듈의 상태가 복잡해질수록 불변성 유지가 어려움    
일반 자바스크립트로 처리하는 것이 더 편할 때는 immer를 사용하지 않아도 됨  

⚠️ 모듈의 상태를 설계할 때는 객체의 깊이가 너무 깊어지지 않도록 주의  
객체의 깊이가 얕을수록 불변성을 지켜 가면서 값을 업데이트하기 수월     

```
yarn add immer
```

```js
import produce from 'immer';
```

### 장점

상황에 따라 상태 값들을 하나의 객체 안에 묶어서 넣는 것이 코드의 가독성을 높이는 데 유리하며, 추후 컴포넌트에 리덕스를 연동할 때도 편리  

* 객체의 구조가 복잡해질 때
* 객체로 이루어진 배열을 다룰 경우 편리하게 상태를 관리할 수 있음  

<br><br>

## useSelector

connect 함수를 사용하지 않고 리덕스 상태를 조회할 수 있음  

```js
const 결과 = useSelector(상태 선택 함수);
// 상태 선택 함수는 mapStateToProps와 동일 형태

// 예시 
const number = useSelector(state => state.counter.number);
```

<br>

### connect 함수와의 차이점

컨테이너 컴포넌트를 만들 때, 편한 것을 사용하면 됨

* connect 함수 사용
* useSelector & useDispatch 사용

connect : 해당 컨테이너 컴포넌트의 부모 컴포넌트가 리렌더링될 때, 해당 컨테이너 컴포넌트의 props가 바뀌지 않았다면 **리렌더링이 자동 방지되어 성능 최적화**  
useSelector : 최적화 작업이 자동으로 이루어지지 않으므로, `React.memo`를 컨테이너 컴포넌트에 사용해야 함

```js
export default React.memo(TodosContainer);
```

<br><br>

## useDispatch

컴포넌트 내부에서 스토어의 내장 함수인 dispatch를 사용할 수 있도록 함    
컨테이너 컴포넌트에서 액션을 디스패치 할 때 사용  

```js
const dispatch = useDispatch();
dispatch({ type: 'SAMPLE_ACTION' });

// 예시 
const dispatch = useDispatch();
const onIncrease = useCallback(() => dispatch(increase()), [dispatch]);
```

💡 성능을 최적화 할 때, **useCallback**으로 액션을 디스패치하는 함수를 감싸기

<br><br>

## useStore

컴포넌트 내부에서 리덕스 스토어 객체를 직접 사용할 수 있음      
⚠️ 스토어에 직접 접근해야 하는 상황에서만 사용(드묾) 

```js
const store = useStore();
store.dispatch({ type: 'SAMPLE_ACTION' });
store.getState();
```

<br><br>

## useActions

여러개의 액션을 사용해야 할 때 깔끔하게 작성 가능        
react-redux에서 제외된 hook이지만, 공식 문서에서 복사해 사용할 수 있음  
> https://react-redux.js.org/api/hooks#recipe-useactions

액션 생성 함수를 액션을 디스패치하는 함수로 변환 

```js
import { bindActionCreators } from 'redux';
import { useDispatch } from 'react-redux';
import { useMemo } from 'react';

export default function useActions(actions, deps) {
  const dispatch = useDispatch();

  return useMemo(
      () => {
          if (Array.isArray(actions)) {
              return actions.map(a => bindActionCreators(a, dispatch));
          }
          return bindActionCreators(actions, dispatch);
        }, 
        deps ? [dispatch, ...deps] : deps,
    );
}
```

* 첫 번째 파라미터는 액션 생성 함수로 이루어진 배열
* 두 번째 파라미터는 deps 배열
  * 이 배열 안에 들어 있는 원소가 바뀌면 액션을 디스패치하는 함수를 새로 생성  
