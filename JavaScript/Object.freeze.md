# Object

## Object.freeze

Object.freeze() 메소드는 객체를 동결   
동결된 객체는 더 이상 변경될 수 없음  
freeze()는 함수에 전달한 객체를 그대로 반환하며, 동결된 객체 사본을 생성하는 것이 아님

* 동결된 객체는 새로운 속성 추가, 존재하는 속성 제거 및 속성 값 변경을 방지 
* 존재하는 속성의 불변성, 설정 가능성(configurability), 작성 가능성이 변경되는 것을 방지
* 동결 객체의 프로토타입 변경도 방지   

<br><br>

## 사용방법

```js
Object.freeze(obj);
```

### 매개변수

* `obj` : 동결할 객체
* `반환 값` : 함수로 전달된 객체와 동일 

<br><br>

## 예시

> 🎯 동결 이후의 변경 시도

* 동결 객체의 속성 집합에는 추가/제거하려는 모든 시도는 조용히 넘어감(조용하게 실패)
* `TypeError` 예외가 발생하며 실패
    * 예외 발생은 보통 엄격 모드(strict mode)인 경우 발생
    * Ex. `'use strict';`
    * 반드시 엄격 모드로만 제한되는 것은 아님
    
<br><br>

## 참고 사이트 

> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze
