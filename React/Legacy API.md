# Legacy API

## isValidElement


isValidElement는 값이 React 엘리먼트인지 확인    
value가 React 엘리먼트인 경우 true를, 그렇지 않으면 false를 반환

```js
const isElement = isValidElement(value);
```

* 42와 같은 숫자는 유효한 React 노드이며 컴포넌트로부터 반환될 수도 있지만,  
유효한 React 엘리먼트는 아님 -> `false`  
* createPortal로 생성된 배열과 포털 역시 React 엘리먼트로 간주되지 않음 -> `false` 

> **리액드 엘리먼트와 리액트 노드의 구분에 주의**
> 
> ⚠️ isValidElement는 인수가 React **엘리먼트**인지를 확인할 뿐, React **노드**인지 여부를 확인하는 것은 아님  
> <em>Ex) 42는 React 엘리먼트는 아니지만, 완전히 유효한 React 노드</em>
> 
> 렌더링할 수 있는지 여부를 확인하는 목적으로 isValidElement를 사용해서는 안 됨 

<br>

### React element

* JSX 태그로 생성한 값 
* `createElement`를 호출하여 생성한 값

<br>

### React node 

* `<div />` 또는 `createElement('div')`로 생성된 React 엘리먼트 
* createPortal로 생성한 포털 
* 문자열 
* 숫자 
* true, false, null, undefined (화면에 표시되지 않음)
* 다른 React 노드로 구성된 배열

<br><br>

## cloneElement

cloneElement를 사용하면 다른 엘리먼트를 시작점으로 사용하여 **새로운 React 엘리먼트를 생성**할 수 있음 

```js
const clonedElement = cloneElement(element, props, ...children)
```

<br>

### 매개변수

* `element` : 유효한 React 엘리먼트  
  * `<Something />`과 같은 JSX 노드, createElement를 호출한 결과, 다른 cloneElement 호출의 결과일 수 있음

* `props` : 객체이거나 null    
  * null을 전달하면 복제된 엘리먼트는 **원본 element.props**를 모두 유지  
  * null이 아닐 경우, 반환된 엘리먼트는 props객체의 모든 prop에 대해 element.props의 값보다 **props의 값을 우선**함   
  나머지 prop들은 원본 element.props에서 채워짐  
  `props.key` 또는 `props.ref`를 전달하면 원래 값을 대체함 

* (선택적) ...`children` : 0개 이상의 자식 노드
  * React 엘리먼트, 문자열, 숫자, portals, 빈 노드(null, undefined, true, false), React 노드의 배열을 포함한 모든 React 노드가 가능
  * ...children 인수를 전달하지 않으면 **원래의 element.props.children이 보존됨** 

<br>

### 반환값

cloneElement는 몇 가지 속성을 가진 React 엘리먼트 객체를 반환

* `type` : element.type과 동일 
* `props` : 재정의되어 전달된 props와 element.props를 얕게 병합한 결과 
* `ref` : props.ref로 재정의되지 않은 경우 원본 element.ref
* `key` : props.key로 재정의되지 않은 경우 원본 element.key

일반적으로 컴포넌트에서 엘리먼트를 반환하거나 다른 엘리먼트의 자식으로 만듦    
엘리먼트의 프로퍼티를 읽을 수는 있지만, 생성된 후에는 모든 엘리먼트를 불명확하게 처리하고 렌더링만 하는 것이 가장 좋음 

<br>

### 주의사항

* 엘리먼트를 복제해도 원본 엘리먼트는 수정되지 않음 
* cloneElement를 사용하면 데이터 흐름을 추적하기가 더 어려워지므로 대신 다른 방법을 사용하는 것이 권장됨 

<br><br>

## 참고 사이트

> https://react-ko.dev/reference/react/cloneElement  
> https://react-ko.dev/reference/react/isValidElement  
> https://react.dev/reference/react/isValidElement
