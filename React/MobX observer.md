# MobX

## observable

observable은 state를 저장하는 추적 가능한 필드를 정의함  
MobX에서는 observable을 기본적으로 사용

* Observable State를 만듬
  * 우리가 관찰하려는 state 
  * state의 변화는 reaction과 computations를 일으킴 
  * 관찰할 수 있는 변화가 일어나면 탐지함 
* 시간에 따라 변할 수 있는 값들을 MobX에게 알려주기 위해

<br><br>

## observer

observer 컴포넌트들은 모든 값을 추적하고 변경사항이 있으면 다시 렌더링  
리액트 컴포넌트를 감싸 사용

* mobx-react 패키지 내부에 존재(mobx core의 일부가 아님)
* 관찰 가능하게 만들어줌

<br><br>

## mobx-react-lite observer

mobx-react-lite 라이브러리의 observer 함수는 기본적으로 함수형 컴포넌트만을 매개변수로 받음
* mobx-react의 observer 함수와 다른점

<br><br>

## 참고 사이트

> https://ko.mobx.js.org/observable-state.html  
> https://ko.mobx.js.org/react-optimizations.html  
> https://kyounghwan01.github.io/blog/React/mobx/basic/#redux%E1%84%8B%E1%85%AA-mobx-%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%B5
