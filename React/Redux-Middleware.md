# Redux-Middleware

## 프로젝트 생성

### 라이브러리 설치

```
yarn add redux react-redux redux-actions
```

<br><br>

## 미들웨어 

액션을 디스패치했을 때, 리듀서에서 처리하기 전에 사전 지정된 작업을 실행   

> `액션` ➡️ `💡미들웨어` ➡️ `리듀서` ➡️ `스토어`

### 미들웨어가 하는 일 

1. 전달받은 액션을 콘솔에 기록하기
2. 전달받은 액션 정보를 기반으로 액션을 취소하기
3. 다른 종류의 액션을 추가로 디스패치하기 

📌 **네트워크 요청 등의 비동기 작업 관리에 매우 유용**

<br><br>

## 미들웨어 생성 

직접 만들어 사용할 일은 드물지만, 직접 만들어보면 미들웨어의 작동 방식을 이해하기 좋음  
원하는 미들웨어를 찾을 수 없을 때는 1. 직접 만들기 2. 기존의 미들웨어를 커스터마이징 

미들웨어는 `함수를 반환하는 함수`를 반환하는 함수  
💡 next를 호출하면 그 다음 처리해야할 미들웨어에게 액션을 넘겨주고, 그 다음 미들웨어가 없다면 리듀서에게 액션을 넘겨줌 

![](../Images/리덕스미들웨어_1.png)

* 미들웨어 내부에서 store.dispatch를 사용하면 첫 번째 미들웨어부터 다시 처리 
* 미들웨어에서 next를 사용하지 않으면 액션이 리듀서에 전달되지 않음 (= 액션이 무시)

```js
const loggerMiddleware = store => next => action => {
  // 미들웨어 기본 구조
};

// 동일 코드
const loggerMiddleware = function loggerMiddleware(store) { // 리덕스 스토어 인스턴스 
  return function(next) { // 함수 형태, store.dispatch와 비슷한 역할 
    return function(action) { // 디스패치된 액션 
      // 미들웨어 기본 구조
    }
  }
}

export default loggerMiddleware;
```

```js
// 스토어 생성 과정에서 적용 
import loggerMiddleware from './lib/loggerMiddleware';

const store = createStore(rootReducer, applyMiddleware(loggerMiddleware));
```

<br>

### 예시

![](../Images/리덕스미들웨어_2.png)

![](../Images/리덕스미들웨어_3.png)

<br><br>

## redux-logger

리덕스 미들웨어를 사용할 때는 미리 완성된 미들웨어를 라이브러리로 설치해 사용하는 경우가 많음  

### 라이브러리 설치

```
yarn add redux-logger
```

```js
// 적용 
import { createLogger } from 'redux-logger';

const logger = createLogger();
const store = createStore(rootReducer, applyMiddleware(logger));
```

![](../Images/리덕스미들웨어_4.png)

* 콘솔에 색상
* 액션 디스패치 시간

<br><br>
