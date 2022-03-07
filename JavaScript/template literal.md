# template literal

## 소개
* 스트링 리터럴 string literal : 문자 그대로
* 템플릿 리터럴 template literal : 템플릿 그대로

<br>

#### 줄바꿈 (공백도 문자취급)
```js
console.log(`a
bb
ccc`)
```
<br>

#### 값 또는 식
```js
const a = 10
const b = 20
const str = `${a} + ${b} = ${ a + b }`
console.log(str)
```
* `` 사이에 ${값 또는 식}   
* 문은 값이 될 수 없어서 불가

<br>

### 특징
1) 줄바꿈 multi-line<br>
2) backtick (`)<br>
3) 문자열 보간(끼워넣기) string interpolation<br> 
   * `${a}`

<br><br>

## 상세

### 1. multi-line의 경우 들여쓰기에 주의

```js
const f = function () {
  const a = `abc
  def
  ghij`
  console.log(a)
}
f()
```
<br>

### 2. ${ } 내에는 `값` 또는 `식`이 올 수 있다.

```js
const counter = {
  current: 0,
  step: 1,
  count: function() { return this.current += this.step },
  reset: function() { return this.current = 0 }
}
console.log(`${counter.count()} ${counter.count()}
${counter.reset()} $${counter.count()}
${counter.count()}$`)
```
<br>

### 3. 결국 문자열이므로, 자동으로 toString 처리가 된다.

```js
console.log(`${[0, 1, 2]}`)
console.log(`${{a:1, b:2}}`)
console.log(`${function(){ return 1 }}`)
console.log(`${(() => 1 )()}` + 1)
```
<br>

### 4. 중첩된 backtick 처리

```js
console.log(`Foo ${`Bar`}`)
console.log(`Foo ${`Bar ${`Baz`}`}`)
```
<br>

### 5. 가독성을 위해 trim 처리

```js
function a () {
  return `
<div>
    <h1>Lorem ipsum.</h1>
</div>
  `.trim()  //return 시작점에 맞춰 trim처리 -> 맨앞과 뒤의 불필요한 공백을 제거 
}
console.log(a())
console.log(a().replace(/\n/g, ''))
```

<br>

'템플릿 리터럴' 단어가 나오게 된 계기

```js
const linesToHTML = function (characters) {
  return characters.reduce(function (charactersResult, character) {
    let {name, lines} = character
    return `${charactersResult || ''}
<article>
  <h1>${name}</h1>
  <ul>
    ${lines.reduce(function (linesResult, line) {
      return `${linesResult || ''}
    <li>${line}</li>
      `.trim()}, 0)}
  </ul>
</article>
  `.trim()}, 0)
}
const characters = [{
  name: 'Aria Stark',
  lines: ['A girl has no name.']
}, {
  name: 'John Snow',
  lines: [
    'You know nothing, John Snow.',
    'Winter is coming.'
  ]
}]
document.body.innerHTML = linesToHTML(characters)
```
* html 태그를 만들어주는 template language / template engine / template library
* 자바스크립트에서도 템플릿 언어의 기능을 비슷하게 구현

<br><br>

## 번외 - forEach, map, reduce

### 1. forEach
for문 돌리기와 같은 개념 <br>

[MDN - Array.prototype.forEach](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

`Array.prototype.forEach(callback[, thisArg])`
- `callback`: `function (currentValue[, index[, originalArray]])`
    - `currentValue`: 현재값 (필수)
    - `index`: 현재 인덱스 
    - `originalArray`: 원본 배열
- `thisArg`: this에 할당할 대상. 생략시 global 객체
* [대괄호]는 생략 가능
* 배열의 모든 메소드는 중요도 순으로 나열되어 있다.


```js
const a = [ 1, 2, 3 ]
a.forEach(function (v, i, arr) {
    console.log(v, i, arr, this)
}, [ 10, 11, 12 ])
```
<br>

### 2. map
for문 돌려서 새로운 배열을 만드는 목적. return 필수<br>

[MDN - Array.prototype.map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

`Array.prototype.map(callback[, thisArg])`
- `callback`: `function (currentValue[, index[, originalArray]])`
    - `currentValue`: 현재값 (필수)
    - `index`: 현재 인덱스
  
<br>

### 3. reduce
for문 돌려서 최종적으로 다른 무언가를 만드는 목적. return 필수<br>

[MDN - Array.prototype.reduce](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

`Array.prototype.reduce(callback[, initialValue])`
- `initialValue`: 초기값. 생략시 첫번째 인자가 자동 지정되며,  
  이 경우 currentValue는 두번째 인자부터 배정된다.
- `callback`: `function (accumulator, currentValue[, currentIndex[, originalArray]])`
    - `accumulator`: 누적된 계산값 (필수)
    - `currentValue`: 현재값 (필수)
    - `currentIndex`: 현재 인덱스
    - `originalArray`: 원본 배열

```js
const arr = [ 1, 2, 3 ]
const res = arr.reduce(function (p, c, i, arr) {
  console.log(p, c, i, arr, this)
  return p + c
}, 10)  
```

```js
const arr = [ 1, 2, 3, 4 ]
const str = arr.reduce(function (res, item, index, array) {
  return res + item
}, '')
console.log(str)  
```

step | res | item | index | array
:-:|:-:|:-:|:-:|:-:
1 | '' | 1 | 0 | [1,2,3,4]
2 | '1' | 2 | 1 | [1,2,3,4]
3 | '12' | 3 | 2 | [1,2,3,4]
4 | '123' | 4 | 3 | [1,2,3,4]
result | '1234' | | |

```js
const arr = [ 'a', 'b', 'c', 'd' ]
const str = arr.reduce(function (res, item, index, array) {
  return res + item
})
console.log(str)
```

step | res | item | index | array
:-:|:-:|:-:|:-:|:-:
1 | 'a' | 'b' | 1 | ['a','b','c','d']
2 | 'ab' | 'c' | 2 | ['a','b','c','d']
3 | 'abc' | 'd' | 3 | ['a','b','c','d']
result | 'abcd' | | |

```js
const arr = [ 10, 20, 30, 40, 50 ]
const r = arr.reduce(function (p, c) {
  return p + c
})
console.log(r)
```

```js
const arr = [ 10, 20, 30, 40, 50 ]
const r = arr.reduce((p, c) => p + c)
console.log(r)
```
- `originalArray`: 원본 배열
- `thisArg`: this에 할당할 대상. 생략시 global객체

```js
const a = [ 1, 2, 3 ]
const b = a.map(function (v, i, arr) {
    console.log(v, i, arr, this)
    return this[0] + v
}, [ 10 ])
```

