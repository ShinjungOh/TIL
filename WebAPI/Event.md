# Event

## Event
EventTarget을 상속하는 모든 요소에 이벤트 핸들러를 등록할 수 있다.

* EventTarget.addEventListener() : 추가
* EventTarget.removeEventListener() : 삭제
* EventTarget.dispatchEvent() : 인공적으로 전달

<br>

>**Events 개념**
https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events

>**Events 종류**
https://developer.mozilla.org/en-US/docs/Web/Events

<br><br>

## bubbling & capturing

* capturing은 거의 사용되지 않는다.

* 버블링이 일어나지 않게 하는 방법 (But 위험해서 사용하지 않는 것이 좋음)
  * event.stopPropagation()
  * event.stopImmediatePropagation()
  * 대신 if (event.target !== event.currentTarget) {return} 사용
  
<br><br>

## 브라우저 기본 기능 취소
* event.preventDefault() : 브라우저에서 기본적으로 발생하는 동작을 취소
* passive : true 의 경우 에러가 뜬다
  * passive : false 로 바꿔서 작동할 수는 있지만 그러지 않는 것이 좋음

<br><br>

## delegation 위임

반복 되는 이벤트를 처리할 때, 부모 안의 자식들에게 공통적으로 무언가를 처리할 때,
일일이 이벤트 리스너를 자식 노드에 추가하기보다 부모에 등록하는 것이 좋다.
