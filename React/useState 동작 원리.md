# React

## useState 

컴포넌트에 state 변수를 추가할 수 있게 해주는 React 훅

```tsx
const [state, setState] = useState(initialState);
```

* 배열 구조 분해를 사용하여 [something, setSomething]과 같은 state 변수의 이름을 지정
* `initialState` : 초기에 state를 설정할 값
  * 이 인자는 초기 렌더링 이후에는 무시됨 

<br>

### 반환값

useState는 정확히 두 개의 값을 가진 배열을 반환  
* 튜플 : 길이와 각 요소마다의 타입이 고정된 배열

1. `state` : 현재 state, `첫 번째 렌더링 중`에는 전달한 `initialState`와 일치
2. `setState` : state를 다른 값으로 업데이트하고 리렌더링을 촉발할 수 있는 set(설정자) 함수

<br>

### set(설정자) 함수 : setSomething(nextState)

useState가 반환하는 `set 함수`를 사용하면 **state를 다른 값으로 업데이트**하고 **리렌더링**을 촉발할 수 있음   

다음 state를 `직접 전달`하거나, 이전 state로부터 계산하여 다음 state를 도출하는 `함수를 전달`할 수도 있음

```tsx
const [name, setName] = useState('Edward');

function handleClick() {
  setName('Taylor');
  setAge(a => a + 1);
  // ...
```

* set 함수는 반환값이 없음, 값을 설정만 해줄 뿐

#### 주의점 

set 함수는 **다음 렌더링에 대한 state 변수만 업데이트**  
set 함수를 호출한 후에도 state 변수에는 여전히 호출 전 화면에 있던 **이전 값**이 담겨 있음    
set 함수를 호출해도 이미 실행 중인 코드의 **현재 state는 변경되지 않음**   

-> state가 스냅샷처럼 동작하기 때문  
state를 업데이트하면 새로운 state 값으로 다른 렌더링을 요청하지만, 이미 실행 중인 이벤트 핸들러의 변수에는 영향을 미치지 않음

<br><br>

## useState 동작 원리

### 배경 

1. 컴포넌트를 만드는 방법에는 `class component`, `function component` 2가지가 존재
2. 함수 컴포넌트로 흐름이 넘어오면서 lifecycle 메소드 대신 `hook`을 사용하게 됨
3. function component는 **불변성**을 가지기 때문에, 컴포넌트가 사용하는 값을 예측 가능하게 해줌 
4. function component는 컴포넌트가 함수의 반환값(return값)으로 나타나며, 그 컴포넌트가 가지고 있는 값, 클로저 등의 정보는 기본적으로 불변
5. 리렌더링이 필요한 경우, function component는 컴포넌트를 만들어주는 함수를 다시 호출함(새로운 컴포넌트) 
6. React hook인 `useState`를 이용해 function component에서도 **상태 관리**를 할 수 있음 

<br>

### Closure

JavaScript가 가진 특징   

어떤 함수에서 선언한 변수(지역 변수)를 참조하는 함수의 내부 함수에서만 발생하는 현상  
내부 함수를 외부로 전달할 경우, 어떤 함수의 LexicalEnvironment가 가비지 컬렉팅 되지 않는 현상

클로저는 함수가 생성될 때 매번 같이 발생  
함수 종료 후에도 사라지지 않는 지역변수를 만들 수 있음

<br>

### 동작 원리

useState의 동작 원리도 `Closure`의 특징을 이용  
Function Component가 실행된 후에도 어떤 변수가 살아서 유지되도록 만들 수 있음 

```tsx
// 첫 렌더링
const [state, setState] = useState(0);

state // state 0
setState(1) // state 0, 한 번 렌더링된 컴포넌트가 가지고 있는 상태값은 중간에 변하지 않음 

// 리렌더링 
state // state 1, 첫 렌더링 때 set 함수로 업데이트한 값을 기억하고 있다가 리렌더링되면서 상태를 업데이트
```

state가 스냅샷처럼 동작하기 때문에 `함수가 호출된 후에도 살아있는 변수`를 이용해 리렌더링 시 업데이트된 state값으로 변경 

<br><br>

## 참고 사이트

> https://react-ko.dev/reference/react/useState  
> https://medium.com/hcleedev/web-usestate%EC%9D%98-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC%EC%99%80-%ED%95%A8%EC%A0%95-7b4825c16b9
