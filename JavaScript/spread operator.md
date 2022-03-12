# spread operator (펼치기 연산자, 전개 연산자)

## 소개

```js
var birds = ['eagle', 'pigeon']
var mammals = ['rabbit', 'cat']
var animals = birds.concat('whale').concat(mammals)
console.log(animals)

const animals2 = [...birds, 'whale', ...mammals]
console.log(animals2)
```

<br><br>

## 상세

### 1. 배열의 각 인자를 펼친 효과

```js
const values = [20, 10, 30, 50, 40]
console.log(20, 10, 30, 50, 40)
console.log(...values)

console.log(Math.max(20, 10, 30, 50, 40))
console.log(Math.max.apply(null, values))
console.log(Math.max(...values))
```

<br>

### 2. 앞뒤로 다른 값들을 함께 사용할 수도 있다.

```js
const values = [3, 4, 5, 6, 7, 8]
const sum = function (...args) {
  return args.reduce(function (p, c) {
    return p + c
  })
}
console.log(sum(1, 2, ...values, 9, 10))
```
* getter : 나머지 rest / 받는 입장 
* setter : 펼치기 spread / 주는 입장

<br>

### 3. iterable한 모든 데이터는 펼칠 수 있다.

```js
const str = 'Hello!'
const splitArr = str.split('')
const restArr = [...str]
console.log(splitArr, restArr)
```
* iterable : 반복할 수 있는

<br>

### 4. push, unshift, concat 등의 기능을 대체할 수 있다.

```js
let originalArr = [2, 3]
const preArr    = [-2, -1]
const sufArr    = [6, 7]

originalArr.unshift(1)  //원래배열
originalArr.push(4)  //원래배열
originalArr = [0, ...originalArr, 5]  //새로운 배열
console.log(originalArr)

const concatArr = preArr.concat(originalArr, sufArr)
const restArr = [...preArr, ...originalArr, ...sufArr]
console.log(concatArr, restArr)
```

<br>

### 5. '새로운' 배열이다.

```js
let originalArray = [1, 2]
let copiedArray = [...originalArray]
console.log(originalArray === copiedArray)

originalArray.push(3)
console.log(originalArray)
console.log(copiedArray)
```

<br>

### 6. '얕은복사'만을 수행한다.

```js
let originalArray = [{
  first: 'Hello,',
  second: 'World!'
}, {
  first: 'Welcome',
  second: 'ES6!'
}]
let copiedArray = [...originalArray]
console.log(originalArray[0].first)

copiedArray[0].first = "Hi,"
console.log(originalArray[0].first)
```

<br><br>

> ## 참고
> - [tc39 propersals](https://github.com/tc39/proposals) : JS 표준 규약을 정의하는 집단
> - [object-rest-spread](https://github.com/tc39/proposal-object-rest-spread)
