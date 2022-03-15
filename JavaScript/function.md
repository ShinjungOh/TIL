# function - etc.

## 1. `name` property of function

```js
function a () { }
console.log(a.name)

const b = function () { }
console.log(b.name)

const c = function cc () { }
console.log(c.name)

const d = () => {}  //익명함수
console.log(d.name)

const e = {
  om1: function () {},
  om2 () {},
  om3: () => {}
}
console.log(e.om1.name, e.om2.name, e.om3.name)

class F {
  static method1 () {}
  method2 () {}
}
const f = new F()
console.log(F.method1.name, f.method2.name)
```

```js
const g = new Function()
console.log(g.name)
```

* name 디버깅시 주로 사용

```js
function a () { }  //함수선언문
const b = function () { }  //함수표현식
const h = a.bind(b)
console.log(h.name)
```

* bind 리액트에서 자주 등장

```js
const person = {
  _name: '재남',
  get name () {
    return this._name
  },
  set name (v) {
    this._name = v
  }
}
const descriptor = Object.getOwnPropertyDescriptor(person, 'name')
console.log(descriptor.get.name)
console.log(descriptor.set.name)
```
<br><br>

## 2. new.target
[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new.target]()

```js
function Person (name) {
  if (this instanceof Person) {
    this.name = name
  } else {  //person을 함수로 호출하면 에러가 나오도록 함
    throw new Error('new 연산자를 사용하세요.')
  }
}
var p1 = new Person('재남')
console.log(p1)

var p2 = Person('성훈')
console.log(p2)  //에러

var p3 = Person.call({}, '곰')
console.log(p3)  //에러

var p4 = Person.call(p1, '곰')
console.log(p4)  //new연산자를 쓰지 않고도 에러가 뜨지 않는 상황 발생 
```
=> new.target 등장

```js
function Person (name) {
  console.dir(new.target)
  if (new.target !== undefined) {
    this.name = name
  } else {
    throw new Error('new 연산자를 사용하세요.')
  }
}

const p1 = new Person('재남')
console.log(p1)

const p2 = Person('성훈')
console.log(p2)

const p3 = Person.call({}, '곰')
console.log(p3)

const p4 = Person.call(p1, '곰')
console.log(p4)  //에러
```

```js
function Person (name) {
  const af = n => {
    this.name = n
    console.log(new.target)
  }
  af(name)
}
const p1 = new Person('재남')
const p2 = Person('성훈')  //undefined
```

```js
function Person (name) {
  this.name = name
}
function Android (name) {
  Person.call(this, name)
}
const p1 = new Android('재남봇')
```
 
<br>

```js
function Person (name) {
  console.log(new.target)
  if (new.target === Person) {
    this.name = name
  } else {
    throw new Error('Person 생성자함수를 new로 호출해야 해요!')
  }
}
function Android (name) {
  Person.call(this, name)
}
const p2 = new Android('재남봇')
```
* 안전장치를 걸 수 있다.

<br><br>

## 3. 블록스코프 내에서의 함수 선언과 호이스팅 (브라우저 비교)

```js
if (true) {
  a()  //true
  function a () { console.log(true) }
}
a()  //true
```

```js
a()
if (true) {
  a()
  function a () { console.log(true) }
}
```
* 브라우저마다 구현 방식이 다름
* es6로 오면서 function이 블록 스코프에 제한될 것인지, 함수 스코프에 제한될 것인지 판단이 달라지는 구간이 있다. 

```js
if (true) {
  a()
  function a () { console.log(true) }
  if (true) {
    a()
    function a () { console.log(false) }
  }
}
a()
```

```js
'use strict'
if (true) {
  a()
  function a () { console.log(true) }
  if (true) {
    a()
    function a () { console.log(false) }
  }
}
a()
```

```js
'use strict'
if (true) {
  function a () { console.log(true) }
  a()
}
a()
```
크롬, 파이어폭스에서는 함수 선언문이 블록 스코프에 갇힌다.

> 해결 : es6에서는 함수선언문을 쓰지 않는다.
  * arrow function 사용
  * 객체 : 메소드 축약형
  * 생성자 함수 : class <br>

=> function은 generator에서만 쓰이게 될 것 (function 키워드가 등장할 일이 없음)

<br>

* strict mode 가 아닌 경우(sloppy mode) : 브라우저마다 동작이 다르다.
* strict mode : 동일하게 동작한다. 함수선언문도 블록 스코프에 갇힌다. 
