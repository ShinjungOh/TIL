# React

## useState 

컴포넌트에 state 변수를 추가할 수 있게 해주는 React 훅

```tsx
const [state, setState] = useState(initialState);
```

* 배열 구조 분해를 사용하여 [something, setSomething]과 같은 state 변수의 이름을 지정
* `initialState` : 초기에 state를 설정할 값
  * 값은 모든 데이터 타입이 허용되지만, 함수에 대해서는 특별한 동작이 있습니다. 
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

* set 함수는 반환값이 없음 

#### 주의점 

set 함수는 **다음 렌더링에 대한 state 변수만 업데이트**  
set 함수를 호출한 후에도 state 변수에는 여전히 호출 전 화면에 있던 **이전 값**이 담겨 있음 

-> state가 스냅샷처럼 동작하기 때문  
state를 업데이트하면 새로운 state 값으로 다른 렌더링을 요청하지만, 이미 실행 중인 이벤트 핸들러의 변수에는 영향을 미치지 않음

<br><br>

## useState 동작 원리


<br><br>

## 참고 사이트

> https://react-ko.dev/reference/react/useState  
> https://medium.com/hcleedev/web-usestate%EC%9D%98-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC%EC%99%80-%ED%95%A8%EC%A0%95-7b4825c16b9
