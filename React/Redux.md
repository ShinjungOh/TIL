# Redux

## 리덕스

리액트 상태 관리 라이브러리    
자바스크립트 앱을 위한 **예측 가능한** 상태 컨테이너(상태 관리)

Flux 패턴, CQRS, Event Sourcing의 개념을 사용해서 만든 라이브러리  
Flux 패턴의 단방향성을 차용했기에 Redux 내에서 발생하는 상태 변화는 모두 예측 가능

컴포넌트의 상태 업데이트 관련 로직을 다른 파일로 분리시켜 효율적으로 관리  
컴포넌트끼리 똑같은 상태를 공유해야 할 때, 여러 컴포넌트를 거치지 않고 상태 값을 전달 또는 업데이트

1. 전역 상태 관리
2. Props drilling 문제 해결

<br>

### Context API vs 리덕스

* 단순한 전역 상태 관리 -> Context API 사용
* 프로젝트 규모가 클 경우 -> 리덕스 사용
    * 리덕스를 사용하면 상태를 더욱 체계적으로 관리할 수 있음

<br>

### 리덕스 장점

* 코드의 유지 보수성 증가
* 작업 효율 극대화
* 개발자 도구 지원
* 미들웨어 기능을 제공, 비동기 작업을 효율적으로 관리

<br><br>

## 리덕스 용어 개념

### 📌 액션

상태에 어떠한 변화가 필요할 때 액션 발생  
하나의 객체로 표현됨

```js
{
    type: 'ADD_TODO', 
    data: {
        id: 1, 
        text: 'redux 학습하기'
    }
}

{
    type: 'CHANGE_INPUT', 
    text: 'Hello'
}
```

* type 필드 - 필수, 액션의 이름
* 그 외의 값 - 작성자 마음대로, 상태 업데이트 시 참고해야 하는 값

<br><br>

### 📌 액션 생성 함수 

액션 객체를 만들어 주는 함수  
어떤 변화를 일으킬 때마다 액션 객체를 만들어야 함 -> 함수로 만들어서 관리

```js
function addTodo(data) {
    return {
        type: 'ADD_TODO',
        data
    }
}

// 화살표 함수
const changeInput = text => ({
  type: 'CHANGE_INPUT',
  text
});
```

<br><br>

### 📌 리듀서

변화를 일으키는 함수  
액션을 만들어서 발생시키면 리듀서가 `현재 상태`와 `전달받은 액션 객체`를 파라미터로 받아 옴  
두 값을 참고해서 `새로운 상태`를 만들어 반환

```js
const initialState = {
    counter: 1
}

function reducer(state = initialState, action) {
    switch (action.type) {
      case INCREMENT: 
          return {
              counter: state.counter + 1
          }
      default: 
          return state;
    }
}
```

<br><br>

### 📌 스토어

프로젝트에 리덕스를 적용하기 위해 스토어를 생성  
한 개의 프로젝트는 **하나의 스토어**만 가짐  
스토어 안에는 현재 애플리케이션 상태, 리듀서, 내장 함수 등

<br><br>

### 📌 디스패치

스토어의 내장 함수 중 하나  
**액션을 발생시키는 것**  
`dispatch(action)` 형태로 액션 객체를 파라미터로 넣어서 호출

디스패치가 호출되면 스토어는 리듀서 함수를 실행시켜서 새로운 상태를 만듦    

<br><br>

### 📌 구독

스토어의 내장 함수 중 하나  
subscribe 함수 안에 리스너 함수를 파라미터로 넣어서 호출하면,  
리스너 함수가 액션이 디스패치되어 상태가 업데이트 될 때마다 호출됨  

```js
const listener = () => {
    console.log('상태가 업데이트됨');
}

const unsubscribe = store.subscribe(listener);

unsubscribe(); // 추후 구독을 비활성화할 때 함수를 호출
```

<br><br>

## 참고 사이트

> https://ko.redux.js.org/introduction/getting-started/  
