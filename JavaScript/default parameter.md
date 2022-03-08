# default parameter (매개변수 기본값)

## 소개
함수의 인자로 넘어오는 것들을 기본값을 지정해줄 수 있음

```js
const f = function (x, y, z) {
  x = x ? x : 4
  y = y || 5
  if (!z) {
    z = 6
  }
  console.log(x, y, z)
}
f(1)  //1 5 6

f(0, null)  //4 5 6
```

```js
const f = function (x, y, z) {
  x = x !== undefined ? x : 3
  y = typeof x !== "undefined" ? y : 4
  console.log(x, y)
}
f(0, null)
```

```js
const f = function (a = 1, b = 2, c = 3, d = 4, e = 5, f = 6) {
  console.log(a, b, c, d, e, f)
}
f(7, 0, "", false, null)  //7 0 '' false null 6
```

<br><br>

## 상세

### 1. undefined 혹은 누락된 파라미터에 대해서만 default parameter가 동작한다.

<br>

### 2. 식

```js
const f = function (x = 1, y = 3 + x) {
  console.log(x, y)
}
f()
```

```js
const getDefault = function () {
  console.log('getDefault Called.')
  return 10
}
const sum = function (x, y = getDefault()) {
  console.log(x + y)
}
sum(1, 2)
sum(1)
```

<br>

### 3. `let` 선언과 동일한 효과

```js
const f = function (x = 1, y = 2 + x) {
  let z = y + 3
  x = 4
  console.log(x, y, z)
}
f()
```
* 디폴트 파라미터에 식이 와도 문제 없다.
* 함수 호출도 올 수 있다.
* 대신 순서가 중요 -> TDZ

### 3-1. TDZ

```js
const multiply = function (x, y = x * 2) {
  console.log(x * y)
}
multiply(2, 3)
multiply(2)
```

```js
const multiply = function (x = y * 3, y) {
  console.log(x, y)
}
multiply(2, 3)
multiply(undefined, 2)
```

### 3-2. 기본값으로 할당하고자 하는 값이 변수일 경우 주의사항

```js
let a = 10
let b = 20
function f (aa = a, b = b) {
  console.log(aa, b)
}
f(1, 2)  //1 2
f(undefined, 2)  //10 2
f(1)  //1 b is not defined(TDZ)
f()
```
* 기본값으로 할달하려는 값이 변수일 경우, 변수명이 달라야 함 (aa, a)

### 3-3. arguments에 영향을 주지 않는다.

```js
const a = function(a = 1, b = 2, c = 3) {
	console.log(arguments)  //유사배열객체
	console.log(a, b, c)
}
a()
a(4)
a(4, 5)
a(4, undefined, 6)
a(4, 5, 6)
```
유사배열객체 array-like object
* 객체인데, 각 프로퍼티의 키가 인덱스이고, length라는 프로퍼티가 있는 객체
* 그렇지만 배열은 아닌 객체  
* arguments는 실제로 넘겨준 값에만 종속된다.
* ES6 환경에서는 arguments 사용x
