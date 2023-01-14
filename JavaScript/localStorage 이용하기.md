# localStorage 이용하기

## localStorage

웹 스토리지 객체인 Storage에 브라우저 내의 key-value 값을 저장 가능  
페이지를 새로 고침하고 브라우저를 다시 실행해도, 세션이 바뀌어도 저장한 데이터 유지

<br>

> `setItem(key, value)` : key, value 추가   
> `getItem(key)` : 키에 해당하는 value 값 받아오기  
> `removeItem(key)` : 키와 해당 값 삭제  
> `clear()` : 모든 것을 삭제 (도메인 내의 localStorage 값 삭제)   
> `key(index)` : 인덱스(index)에 해당하는 key 값 받아오기   
> `length` : 전체 item 갯수  

<br><br>

## localStorage에 아이템 추가, 읽기  

* `window.localStorage.setItem(key, value)`
* `window.localStorage.getItem(key)`

<br>

```js
// setItem() 함수를 사용해 localStorage에 key-value를 저장
window.localStorage.setItem('name', 'anna');
window.localStorage.setItem('age', '20');

// getItem() 함수에 key를 전달하여 localStorage에 저장된 값을 읽어오기
window.localStorage.getItem('name');
window.localStorage.getItem('age');
```

⚠️ localStorage는 문자열만을 저장  
숫자로 저장하더라도, 문자열로 저장됨 

JSON.stringify() 함수를 사용해 객체와 배열을 JSON 문자열로 변환해야 함

object -> string 으로 변환하는 방법 : `JSON.stringify(object name)`  
string -> object 로 변환하는 방법 : `JSON.parse(localstorage key)`

<br><br>

## localStorage에 값 삭제하기  

`window.localStorage.removeItem(key)`

```js
// removeItem() 함수를 사용해 key가 'name'인 아이템을 삭제
window.localStorage.removeItem('name');
```

<br><br>

## localStorage에 값 전체 삭제하기  

`window.localStorage.clear()`

<br><br>

## localStorage의 아이템 갯수 구하기  

`window.localStorage.length`

<br><br>

## localStorage의 key 이름 찾기  

`window.localStorage.key(index)`

<br><br>

## 참고 사이트

> https://ko.javascript.info/localstorage    
> https://hianna.tistory.com/697
