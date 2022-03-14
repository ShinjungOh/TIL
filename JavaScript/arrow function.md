# Arrow Function

## 소개

```js
var a = function () {
  return new Date()
}
var b = function (a) {
  return a * a
}
var c = function (a, b) {
  return a + b
}
var d = function (a, b) {
  console.log( a * b )
}
```

```js
let a = () => new Date()
let b = a => a * a
let c = (a, b) => a + b
let d = (a, b) => {
  console.log( a * b )
}
```
<br>

## 상세

### 1. (매개변수) => { 본문 }

<br>

### 2. 매개변수가 하나뿐인 경우 괄호 생략 가능
    let b = a => a * a

<br>

### 3. 매개변수가 없을 경우엔 괄호 필수
    let a = () => new Date()
    let a = _ => new Date()  //_를 사용하기도 하지만 좋은 습관은 아니다.


<br>

### 4. 본문이 `return [식 or 값]` 뿐인 경우 `{ }`와 `return` 키워드 생략 가능

<br>

### 5. 위 4. 에서 return할 값이 `객체`인 경우엔 괄호 필수

```js
const f = () => {
  a: 1,
  b: 2
}

const f = () => ({
  a: 1,
  b: 2
})
```
* 중괄호 표시를 객체가 아닌 함수 본문으로 인식할 것이기 때문

<br>

### 6. 실행컨텍스트 생성시 this 바인딩을 하지 않음

```js
const obj = {
  a: function () {
    console.log(this)

    const b = () => {
      console.log(this)
    }

    b()
  }
}
obj.a()
```
기존 함수와의 차이점
* arrow function은 함수 스코프
* <strong>arrow function은 실행 컨텍스트가 실행될 때 this 바인딩 작업을 하지 않음</strong>
* this 바인딩하지 않는 것 : 블록 스코프 (arrow function은 블록 스코프가 아니다.)

```js
const obj = {
  grades: [80, 90, 100],
  getTotal: function () {
    this.total = 0
    this.grades.forEach(function(v) {
      this.total += v
    })
  }
}
obj.getTotal()
console.log(obj.total)
```

<br>

### 7. 명시적 this 바인딩 ?

```js
const a = () => {
  console.log(this)
}
a.call({a: 1})
```

```js
const a = (...rest) => {
  console.log(this, rest)
}
a.call({a: 1}, 1, 2, 3)
a.apply([], [4, 5, 6])
const b = a.bind(null, 7, 8, 9, 10)
b()
```

```js
const obj = {
  f() {
    const a = (...rest) => {
      console.log(this, rest)
    }
    a.call({a: 1}, 1, 2, 3)
    a.apply([], [4, 5, 6])
    const b = a.bind(null, 7, 8, 9, 10)
    b()
  }
}
obj.f()
```

<br>

### 8. 생성자함수로 쓸 수 없음

```js
const P = (name) => {
  this.name = name
}
const j = new P('재남')

console.dir(P)
```
* concise method, arrow function 둘 다 prototype 프로퍼티가 없다.
* 공통점
  1. 생성자 함수로 쓸 수 없다.
  2. arguments, callee -> 숨겨져 있다. invoke 해야만 값을 얻을 수 있다.
* 차이점
    1. 메소드는 메소드로만 사용 가능 (함수로서 불가)
    2. 함수는 함수로만 사용 가능 

<br>

### 9. 그밖에

this 외에도 super, arguments, new.target 등을 바인딩하지 않는다.
