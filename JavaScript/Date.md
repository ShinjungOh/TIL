# Date

## 생성자

### `Date`

함수로 호출할 경우 `new Date().toString()`과 동일하게 **현재 날짜와 시간을 나타내는 문자열**을 반환

### `new Date`

생성자로 호출할 경우 **새로운 Date 객체를 반환**

<br><br>

## 정적 메소드

### `Date.now`

1970년 1월 1일 00:00:00 UTC로부터 지난 시간을 **밀리초 단위의 숫자 값**으로 반환   
윤초는 무시

### `Date.parse`

날짜를 나타내는 문자열을 분석한 후, 해당 날짜와 1970년 1월 1일 00:00:00 UTC의 시간 차이를 **밀리초 단위의 숫자 값**으로 반환

* ⚠️ Date.parse를 사용한 날짜 분석은 **브라우저 간 차이 및 일관적이지 못한 동작**을 가지고 있으므로 사용하지 않는 것이 좋음 

### `Date.UTC`

생성자가 받을 수 있는 제일 많은 매개변수(구성요소 각각, 2개~7개)를 동일하게 받아서, 
1970년 1월 1일 00:00:00 UTC의 시간 차이를 **밀리초 단위의 숫자 값**으로 반환  
윤초는 무시

<br><br>

## 참고 사이트

> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date  
> https://ko.javascript.info/date  
