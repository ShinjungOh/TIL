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


