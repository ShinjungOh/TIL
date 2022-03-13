# enhanced object functionalities (객체의 향상된 기능들)

## 1️⃣ shorthand properties (프로퍼티 축약)

## 소개

```js
var x = 10
var y = 20
var obj = {
  x: x,
  y: y
}
```

```js
const x = 10
const y = 20
const obj = {
  x,  //key이자 value
  y
}
```

<br>

## 상세

프로퍼티의 key와 value에 할당할 변수명이 동일한 경우 value 생략 가능

<br>

## 활용

### 1. 함수에서 객체를 리턴할 때

```js
const convertExtension = function (fullFileName) {
  const fullFileNameArr = fullFileName.split('.')
  const filename = fullFileNameArr[0]
  const ext = fullFileNameArr[1] && fullFileNameArr[1] === 'png' ? 'jpg' : 'gif'
  return {
    filename,
    ext
  }
}
convertExtension('abc.png')
```

<br>

### 2. destructuring assignment

```js
const {
  name,
  age
} = {
  name: '재남',
  age: 30
}
console.log(name, age)
```

<br><br>


## 2️⃣ concise methods (간결한 메소드)

## 소개

```js
var obj = {
  name: 'foo',
  getName: function () { return this.name }
}
```

```js
const obj = {
  name: 'foo',
  getName () { return this.name }
}
```

<br>

## 상세

### 1. `:function` 키워드 제거

<br>

### 2. `super` 명렁어로 상위 클래스에 접근 가능

```js
const Person = {
  greeting: function () { return 'hello' }
}
const friend = {
  greeting: function () {
    return 'hi, ' + super.greeting()
  }
}
Object.setPrototypeOf(friend, Person)
friend.greeting()
```

```js
const Person = {
  greeting () { return 'hello' }
}
const friend = {
  greeting () {
    return 'hi, ' + super.greeting()  //super
  }
}
Object.setPrototypeOf(friend, Person)  //friend를 인스턴스로, person을 생성자 함수로 지정하라
friend.greeting()
```

<br>

### 3. `prototype` 프로퍼티가 없음 -> 생성자함수로 쓸 수 없음

```js
const Person = {
  greeting () { return 'hello' }
}
const p = new Person.greeting()
```
* 생성자 함수로서의 기능을 제한시킴
* 함수 본연의 기능만 가능
* prototype 프로퍼티가 없어서 가벼워지고 성능 상승

<br>

### 4. 그밖에는 모두 기존 함수/메소드와 동일

```js
const obj = {
  a () { console.log('obj log') },
  log () { console.log(this) }
}
console.log(obj.a.name)
setTimeout(obj.a, 1000)
obj.log()
obj.log.call([])
setTimeout(obj.log.bind('haha'), 2000)
```

<br><br>

## 3️⃣ computed property name (계산된 프로퍼티명)

## 소개

```js
var className = ' Class'
var obj = {}

obj.'ab cd' = 'AB CD'  //.이후 문자열 불가

obj = {
  'ab cd': 'AB CD'  //가능
}

obj['ab cd'] = 'AB CD'  //[] 대괄호 표기법 사용해야 함

var obj = {
  'A' + className: 'A급'  //불가. 에러
}

obj['A' + className] = 'A급'  //가능

const obj2 = {
  'ab cd':
  ['A' + className]: 'A급'
}
```

```js
let suffix = ' name'
let iu = {
  ['last' + suffix]: '이',
  ['first' + suffix]: '지은'
}
console.log(iu)
```

```js
const count = (function (c) {
  return function () {
    return c++
  }
})(0)
var obj = {
  [`a_${count()}`]: count(),
  [`a_${count()}`]: count(),
  [`a_${count()}`]: count()
}
console.log(obj)
```

<br>

## 상세

### 1. 객체 리터럴 선언시 프로퍼티 키값에 대괄호 표기로 접근 가능

<br>

### 2. 대괄호 내에는 값 또는 식을 넣어 조합할 수 있음
* 문 불가

<br><br>

## 4️⃣ own property enumeration order (고정된 프로퍼티 열거 순서)

```js
const obj1 = {
  c: 1,
  2: 2,
  a: 3,
  0: 4,
  b: 5,
  1: 6
}
const keys1 = []
for (const key in obj1) {
  keys1.push(key)
}
console.log(keys1)  //0 1 2 c a b
console.log(Object.keys(obj1))  //0 1 2 c a b
console.log(Object.getOwnPropertyNames(obj1))  //0 1 2 c a b
```
* 숫자가 먼저 오고, 작은 수에서 큰 수의 순서로, 문자열이 입력된 순서 그대로 나열

```js
const obj2 = {
  [Symbol('2')]: true,
  '02': true,
  '10': true,
  '01': true,
  '2': true,
  [Symbol('1')]: true
}
const keys2= []
for(const key in obj2) {
  keys2.push(key)
}
console.log(keys2)  //2 10 02 01. 첫글자에 0이 들어가면 문자열
console.log(Object.keys(obj2))
console.log(Object.getOwnPropertyNames(obj2))
console.log(Reflect.ownKeys(obj2))
```
* 숫자인데 첫글자가 0이 아닌 경우 -> 숫자로 인식
* 0은 숫자로 인식

```js
const obj3 = Object.assign({}, obj1, obj2)
const keys3= []
for(const key in obj3) {
  keys3.push(key)
}
console.log(keys3)  //0 1 2 10 c a b 02 01
console.log(Object.keys(obj3))  //0 1 2 10 c a b 02 01
console.log(Object.getOwnPropertyNames(obj3))  //0 1 2 10 c a b 02 01
console.log(Reflect.ownKeys(obj3))  //0 1 2 10 c a b 02 01 symbol(2) symbol(1) 
```
* symbol은 열거 대상에서 제외됨 -> 열거하려면 `Reflect.ownKeys` 

<br>

### 1. 열거순서는 다음 규칙을 따른다.

- **number &rarr string &rarr symbol** 의 순서로 정렬된다.
- `number` key는 프로퍼티들 중 가장 앞에 위치하며, 오름차순이다.
- `string` key는 객체에 추가된 당시의 순서를 유지하면서 숫자 뒤에 위치한다.
- `Symbol` key는 객체에 추가된 당시의 순서를 유지하면서 제일 마지막에 위치한다.
- `숫자` 오름차순 - `문자열` 입력된 순서 - `심볼` 입력된 순서

<br>

### 2. number(index)로 인식하는 key는 다음과 같다.

- 0 이상의, 첫째자리가 0이 아닌 수는, 문자열로 입력해도 똑같이 숫자로 인식한다.
- 첫째자리가 0인 두자리 이상의 숫자는 문자열로 입력해야 하고, 문자열로 인식한다.
- 음수는 문자열로 입력해야 하고, 문자열로 인식한다.

**&there4; 'index'로 인식할 수 있는 경우에 한해서만 작은 수부터 나열한다.**

<br>

### 3. 열거순서를 엄격히 지키는 경우는 다음과 같다.

- `Object.getOwnPropertyNames()`
- `Reflect.ownKeys()`
- `Object.assign()`

<br>

### 4. ES5 하위문법인 다음의 경우에는 정합성을 보장하지 않는다.

- `for in`
- `Object.keys()`
- `JSON.stringify()`
- 어떤 환경인가에 따라 출력결과가 달라질 수 있다.