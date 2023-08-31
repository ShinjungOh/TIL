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

### React element

* JSX 태그로 생성한 값 
* `createElement`를 호출하여 생성한 값

### React node 

* `<div />` 또는 `createElement('div')`로 생성된 React 엘리먼트 
* createPortal로 생성한 포털 
* 문자열 
* 숫자 
* true, false, null, undefined (화면에 표시되지 않음)
* 다른 React 노드로 구성된 배열

<br><br>


## 참고 사이트

> https://react-ko.dev/reference/react/cloneElement  
> https://react-ko.dev/reference/react/isValidElement  
> https://react.dev/reference/react/isValidElement
