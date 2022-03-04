# Variables

## let

```js
let a = 1
function f () {
  console.log(a, b, c)  //b, c is not defined
	let b = 2
	console.log(a, b, c)  //c is not defined
	if (true) {
		let c = 3
		console.log(a, b, c)  //1 2 3
	}
	console.log(a, b, c)  //c is not defined
}
f()
```
```js
for (let i = 0; i < 5; i++) {
  console.log(i)
}
console.log(i)
```

<br>

### 재할당 가능

```js
let a = 1
a = 2  //재할당
console.log(a)
```

* let은 var와 같은 개념이되, 블록 스코프에 갇힌다.
* TDZ가 존재한다.

<br>

### 반복문 내에서의 함수 실행시

```js
var funcs = []
for (var i = 0; i < 10; i++) {
  funcs.push(function () {
    console.log(i)
  })
}
funcs.forEach(function (f) {
  f()
})  //10 * 10
```

```js
var funcs = []
for (var i = 0; i < 10; i++) {
  funcs.push((function (v) {
    return function () {  //i를 넘겨주기 위해 즉시실행함수로 만든다.
      console.log(v)
    }
  })(i))
}
funcs.forEach(function (f) {
  f()
})  
```

```js
let funcs = []
for (let i = 0; i < 10; i++) {
  funcs.push(function () {
	  console.log(i)  //i값이 블록 스코프 내에 존재
  })
}
funcs.forEach(function (f) {
  f()
})
```
* for문 자체가 블록 스코프
* 즉시실행함수를 고민할 필요가 적어져서 메모리 소모를 덜 할 수 있다.
* 클로저 안에서 선언된 변수는 영원하다.

<br><br>

## const

* constant variable (상수 변수)의 약자
* constant : 상수 

<br>

### 재할당
```js
const PI = 3.141593
PI = 3.14
```
* 재할당 불가

<br>

### 최초 선언시 할당하지 않으면

```js
const PI
PI = 3.14
```
* 상수는 무조건 선언과 동시에 값을 할당해야함

<br>

### 참조타입 데이터의 경우

```js
const OBJ = {
  prop1 : 1,
  prop2 : 2
}
OBJ.prop1 = 3  //OBJ 내부의 프로퍼티에 접근. OBJ는 공간을 참조하는 것
console.log(OBJ.prop1)
```

```js
const ARR = [0, 1, 2]
ARR.push(3)  //내부에 접근 가능
delete ARR[1]  //내부에 접근 가능
console.log(ARR)
```

* 참조형 데이터를 상수변수에 할당할 경우에는, 
참조형 데이터 내부에 있는 프로퍼티들은 상수가 아니다.

<br>

내부의 것들도 상수로 만들고 싶다면?
> 해결방안: `Object.freeze()`, `Object.defineProperty()`

```js
const OBJ = {}
Object.defineProperty(OBJ, 'prop1', {
  value : 1,
  writable: false,
  configurable: false
})

const OBJ2 = {
  prop1 : 1
}
Object.freeze(OBJ2)  //프로퍼티를 얼려라
```
<br>

> 여전히 남는 문제점: nested Object의 경우

```js
const OBJ = {
  prop1 : 1,
  prop2 : [2, 3, 4],
  prop3 : { a: 1, b: 2 }
}
Object.freeze(OBJ)
OBJ.prop1 = 3
OBJ.prop2.push(5)
OBJ.prop3.b = 3
console.log(OBJ)

Object.freeze(OBJ.prop2)
OBJ.prop2.push(6)
console.log(OBJ)
```

<br>

* 모든 프로퍼티를 얼리고 싶을 경우
1. obj 객체 자체를 얼린다.
2. obj 내부의 프로퍼티들을 순회하면서, 참조형일 경우 1) 반복 -> 재귀 <br>
=> DeepFreezing <br>

* 깊은 복사를 해야만 immutable 하다.
* ⭐️<strong>불변객체(immutable object)</strong> 
  * 매번 새로운 객체 생성. 깊은 복사 deep copy 해야 함
  * 생성 후 그 상태를 바꿀 수 없는 객체

<br>

### 반복문 내부에서의 상수
for문에서의 주의사항

```js
var obj = {
  prop1: 1,
  prop2: 2,
  prop3: 3
}
for (const prop in obj) {
  console.log(prop)  //작동함. 암기가 필요
}
```

```js
for (const i = 0; i < 5; i++) {
  console.log(i)  //Assignment to constant variable.
}
```
* for문의 기본적인 형태에서는 const를 쓰면 안됨

<br><br>

## let, const 공통사항

### 유효범위
블록 스코프 내부

```js
{
  let a = 10
  {
    const b = 20
    console.log(b)
  }
  console.log(a)
  console.log(b)
}
console.log(a)
```

<br>

### 재선언 (재정의)

```js
var a = 0
var a = 1
console.log(a)

let b = 2
let b = 3
console.log(b)  //Identifier 'b' has already been declared

const c = 4
const c = 5
console.log(c)  //Identifier 'c' has already been declared

var d = 4
let d = 5
const d = 6
console.log(d)  //Identifier 'd' has already been declared
```
* ES6 환경에서는 var를 잊어버릴 것
* let, const만 사용 
  * 둘은 목적이 다름
  * 주로 const를 사용할 것 <br>
<br>
* let : 값 자체의 변경이 필요한 예외적인 경우
* const -> 객체 
  * 객체 내부의 프로퍼티를 바꾸는 것은 언제든지 가능
  * 안전함 : 값을 바꾸려고 할 때 보호

<br>

### 초기화되기 전 호출
-> 에러 발생
```js
{
  console.log(a)
  let a = 10
  {
    console.log(b)
    let b = 20
  }
}

{
  console.log(a)
  const a = 10
  {
    console.log(b)
    const b = 20
  }
}
```
=> hoisting X ?

<br>

### TDZ (Temporal Dead Zone, 임시사각지대)

```js
{
  let a = 10
  {
    console.log(a)
    let a = 20
  }
}
```

```js
{
  const a = 10
  console.log(a)
  {
    console.log(a)
    const a = 20
    console.log(a)
  }
}
```

<br>

### 전역객체의 프로퍼티

```js
var a = 10
console.log(window.a)  //10
console.log(a)  //10
delete a
console.log(window.a)  //10
console.log(a)  //10

window.b = 20
console.log(window.b)
console.log(b)
delete b
console.log(window.b)
console.log(b)

let c = 30
console.log(window.c)
console.log(c)
delete c
console.log(window.c)
console.log(c)

const d = 40
console.log(window.d)
console.log(d)
delete d
console.log(window.d)
console.log(d)
```
* 전역공간에서 var로 선언한 변수는 전역변수임과 동시에 전역객체의 프로퍼티가 됨 -> 함부로 삭제할 수 없음
* let, const : 전역객체의 공간과 전역변수는 별개로 동작하게 됨
