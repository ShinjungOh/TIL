# Symbol

## 소개

- primitive value! => 유일무이하고 고유한 존재
- 비공개 멤버에 대한 needs에서 탄생
- 기본적인 열거대상에서 제외
- 암묵적 형변환 불가(숫자형, 문자형으로 형변환 불가)
 
<br>

`기본형 primitive value` <br>
number, string, boolean, null, undefined, symbol

`참조형 reference value` <br>
object ,array ,function ,map ,set ,weakmap ,weakset


<br>

### 1. 만들기

* `Symbol([string])` : 문자열이 아닌 타입은 자동으로 toString 처리
* new 연산자 사용 불가
* [] 생략 가능. 문자열이 와도 되고 안와도 됨

```js
const sb1 = Symbol()
const sb2 = Symbol()
console.log(sb1, sb2)
console.log(sb1 === sb2)  //같지 않다
``` 

```js
const sb1 = Symbol('symbol')
const sb2 = Symbol('symbol')
console.log(sb1, sb2)
console.log(sb1 === sb2)  //같지 않다
```

```js
const obj = { a: 1 }
const sb1 = Symbol(obj)
const sb2 = Symbol(obj)
console.log(sb1, sb2)
console.log(sb1 === sb2)
```
* 문자열이 아닌 타입은 자동으로 toString 처리

```js
const sb = Symbol(null)
console.log(typeof sb)
```
<br>

### 2. 객체 프로퍼티의 키로 활용

```js
const NAME = Symbol('이름')
const GENDER = Symbol('성별')
const iu = {
  [NAME]: '아이유',
  [GENDER]: 'female',
  age: 26
}
const suzi = {
  [NAME]: '수지',
  [GENDER]: 'female',
  age: 26
}
const jn = {
  [NAME]: '재남',
  [GENDER]: 'male',
  age: 30
}

console.log(iu, suzi, jn)
```
* 대괄호 표기법 사용

<br>

### 3. 프로퍼티 키로 할당한 심볼 탐색 (접근)

```js
console.log(iu[NAME], suzi[NAME], jn[NAME])

for (const prop in iu) {
  console.log(prop, iu[prop])
}

Object.keys(iu).forEach(k => {
  console.log(k, iu[k])
})

Object.getOwnPropertyNames(iu).forEach(k => {
  console.log(k, iu[k])
})

Object.getOwnPropertySymbols(iu).forEach(k => {
  console.log(k, iu[k])
})

Reflect.ownKeys(iu).forEach(k => {
  console.log(k, iu[k])  //key 전부 반환
})
```
* `getOwnPropertySymbols`, `Reflect.ownKeys` 두가지만 심볼에 접근 가능 

<br>

### 4. private member 만들기

```js
const obj = (() => {
  const _privateMember1 = Symbol('private1')
  const _privateMember2 = Symbol('private1')
  return {
    [_privateMember1]: '외부에서 보이긴 하는데 접근할 방법이 마땅찮네',
    [_privateMember2]: 10,
    publicMember1: 20,
    publicMember2: 30
  }
})()
console.log(obj)
console.log(obj[Symbol('private1')])  //접근 불가
console.log(obj[_privateMember1])  //접근 불가

for (const prop in obj) {
  console.log(prop, obj[prop])  //접근 불가
}

Object.keys(obj).forEach(k => {
  console.log(k, obj[k])  //접근 불가
})

Object.getOwnPropertyNames(obj).forEach(k => {
  console.log(k, obj[k])  //접근 불가
})

// 물론 아래 방법들로는 접근 가능하나...
Object.getOwnPropertySymbols(obj).forEach(k => {
  console.log(k, obj[k])
})

Reflect.ownKeys(obj).forEach(k => {
  console.log(k, obj[k])
})
```
* symbol을 활용하면 자바스크립트에서도 private member를 흉내낼 수 있다
* 캡슐화의 목적 : 실수 방지 (외부에서 접근하지 못하도록)

<br><br>

## `Symbol.for` - 공유심볼

- public member! 전역공간에서 공유되는 심볼
- private member와 정반대 개념
- 스코프에 갇히지 않음


```js
const COMMON1 = Symbol.for('공유심볼')
const obj = {
  [COMMON1]: '공유할 프로퍼티 키값이에요. 어디서든 접근 가능하답니다.'
}
console.log(obj[COMMON1])

const COMMON2 = Symbol.for('공유심볼')
console.log(obj[COMMON2])

console.log(COMMON1 === COMMON2)  //같음

const UNCOMMON = Symbol('비공유심볼')
const commonSymbolKey1 = Symbol.keyFor(COMMON1)  //공유심볼
const commonSymbolKey2 = Symbol.keyFor(COMMON2)  //공유심볼
const commonSymbolKey2 = Symbol.keyFor(UNCOMMON)  
```
* 비공유심볼은 keyfor 메소드 사용 불가

```js
const obj = (() => {
  const COMMON1 = Symbol.for('공유심볼')
  return {
    [COMMON1]: '공유할 프로퍼티 키값이에요. 어디서든 접근 가능하답니다.'
  }
})()
const COMMON2 = Symbol.for('공유심볼')
console.log(obj[COMMON2])
```
* 용도 : 프로젝트를 진행시 공용으로 쓰이는 값을 저장할 때 

<br><br>

## 표준 심볼

- Symbol.hasInstance:  
  `instance instanceof constructor` 명령은 내부적으로 `constructor[Symbol.hasInstance](instance)` 으로 동작
- Symbol.isConcatSpreadable:  
  array의 `concat` 메소드에 인자로 넘길 때 이를 flatten할지 여부를 가리키는 boolean값 (default: true)


```js
const arr = [4, 5, 6]
arr[Symbol.isConcatSpreadable] = true
console.log([1, 2, 3].concat(arr))  //1 2 3 4 5 6

arr[Symbol.isConcatSpreadable] = false
console.log([1, 2, 3].concat(arr))  //1 2 3 array(3)-펼쳐지지 않음
```

<BR>

원래 있던 기능을 다르게 사용할 수 있도록 제공
- Symbol.iterator: 추후 다룸
- Symbol.match: 정규표현식 및 문자열 관련
- Symbol.replace: 정규표현식 및 문자열 관련
- Symbol.search: 정규표현식 및 문자열 관련
- Symbol.species: 파생클래스를 만들기 위한 생성자
- Symbol.split: 문자열을 나누는 조건 설정

```js
const str = '이 _ 문자열을 _ 이렇게 _ 나누어주었으면 _ 좋겠어.'
String.prototype[Symbol.split] = function (string) {
  let result = ''
  let residue = string
  let index = 0
  do {
    index = residue.indexOf(this)
    if(index <= -1) {
      break
    }
    result += residue.substr(0, index) + '/'
    residue = residue.substr(index + this.length)
  } while (true)
  result += residue
  return result
}
console.log(str.split(' _ '))
```

<BR>

- Symbol.toStringTag: `Object.prototype.toString`이 호출되었을 때 어떤 명칭을 반환할 지를 지정 가능
- class의 이름을 지정 가능

```js
class Person {
  constructor (name) { this.name = name }
}
const jn = new Person('재남')
console.log(jn.toString())  //object object

Person.prototype[Symbol.toStringTag] = 'PERSON'
console.log(jn.toString())  //object PERSON
```
<BR>

- Symbol.unscopables: with문과 관련
- 스코프에 종속될 것인지, 아닌지를 선택할 수 있게끔 바꿔주는 것

> 표준 심볼들의 의의 : 해당 심볼을 재정의함으로써 기존에는 표준객체 내부 전용이던 기능들을 개발자의 입맛에 맞게 바꾸어 쓸 수 있게 되었음
