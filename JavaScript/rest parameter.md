# rest parameter (나머지 매개변수)

## 소개

```js
function foo (a, b) {
  a = 1
  arguments[0] = 2
  console.log(a, arguments[0])  //a: 1 2  //arguments[0]: 2
}
foo(10, 20)
```

```js
function f (x, y) {  //매개변수. 파라미터 
  var rest = Array.prototype.slice.call(arguments, 2)
  console.log(rest)
}
f(1, 2, true, null, undefined, 10)
```

```js
const f = function (x, y, ...rest) {
  console.log(rest)
}
f(1, 2, true, null, undefined, 10)
```
* '...'는 마지막에 와야 한다.

<br><br>

## 상세

### 1. `...[매개변수명]`

<br>

### 2. 오직 한 번, 매개변수의 가장 마지막에서만

```js
const f = function (_first, ...rest, _last) {  //오 
  console.log(_first, _last)
}
f(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
```
<br>

### 3. 객체의 setter에서

```js
let person = {
  name: 'name',
  age : 30,
  get personInfo(){
    return this.name + ' ' + this.age
  },
  set personInfo (...val) {
    this.name = val[0]
    this.age  = val[1]
  }
}
console.log(person.personInfo)
```
* '...' 사용 불가 : 값을 여러개 넣어도 의미가 없음

<br>

### 4. `arguments`를 대체

```js
function argsAlternate (...args) {
  console.log(args.length, arguments.length)
  console.log(args[0], arguments[0])
  console.log(args[args.length - 1], arguments[arguments.length - 1])
  args[1] = 10
  arguments[1] = 20
  console.log(args[1], arguments[1])
}
argsAlternate(1, 2, 3, 4)
```
