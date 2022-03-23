# Iterable, Iterator

## Iterable

내부 요소들을 공개적으로 탐색(반복)할 수 있는 데이터 구조  
[Symbol.iterator] 메소드를 가지고 있다.

```js
const arr = ['a', 'b', 'c']
const set = new Set(['a', 'b', 'c'])
const map = new Map([[false, 'no'], [true, 'yes'], ['well', 'soso']])
const str = '문자열도 이터러블하다!?!!'
```

<br>

### 1️⃣ 개체 자신이 iterable한 경우

### 1. array, map, set, string

<br>

### 2. `[Symbol.iterator]` 메소드가 존재하는 모든 개체

```js
console.dir([1, 2, 3])
console.dir(new Set([1, 2, 3]))
console.dir(new Map([[0, 1], [1, 2], [2, 3]]))
```

- 없는 경우
    ```js
    const obj = { 0: 1, 1: 2, 2: 3, length: 3 }  //유사배열객체
    console.dir(obj)
    ```

<br>

### 3. `generator`를 호출한 결과

```js
function* generator () {
  yield 1
  yield 2
  yield 3
}
const gene = generator()
console.dir(gene)
```
<br>

### 2️⃣ iterable한 개체의 특징

```js
const arr = [1, 2, 3]
const map = new Map([['a', 1], ['b', 2], ['c', 3]])
const set = new Set([1, 2, 3])
const str = '이런것도 된다.'
const gene = (function* () {
  yield 1
  yield 2
  yield 3
})()
```
<br>

### 1. Array.from 메소드로 배열로 전환 가능

```js
const arrFromArr1 = Array.from(arr)
const arrFromMap1 = Array.from(map)
const arrFromSet1 = Array.from(set)
const arrFromStr1 = Array.from(str)
const arrFromGene1 = Array.from(gene)
```
* iterable한 객체가 들어오면 배열로 변환해준다

<br>

### 2. spread operator로 배열로 전환 가능

```js
const arrFromArr2 = [...arr]
const arrFromMap2 = [...map]
const arrFromSet2 = [...set]
const arrFromStr2 = [...str]
const arrFromGene2 = [...gene]
```
<br>

### 3. 해체할당 가능

```js
const [arrA, , arrC] = arr
const [mapA, , mapC] = map
const [ , setB, setC] = set
const [ , strB, ...strRest] = str
const [geneA, ...geneRest] = gene
console.log(arrA, arrC)
console.log(mapA, mapC)
console.log(setB, setC)
console.log(strB, strRest)
console.log(geneA, geneRest)
```
* iterable한 것은 모두 Symbol.iterator를 들고 있다
* .next() => 반복호출. done이 true가 되기 전까


<br>

### 4. for ... of 명령 수행 가능

```js
for (const x of arr) {
  console.log(x)
}
for (const x of map) {
  console.log(x)
}
for (const x of set) {
  console.log(x)
}
for (const x of str) {
  console.log(x)
}
for (const x of gene) {
  console.log(x)
}
```
<br>

### 5. `Promise.all`, `Promise.race` 명령 수행 가능

```js
const a = [
  new Promise((resolve, reject) => { setTimeout(resolve, 500, 1) }),
  new Promise((resolve, reject) => { setTimeout(resolve, 100, 2) }),
  3456,
  'abc',
  new Promise((resolve, reject) => { setTimeout(resolve, 300, 3) }),
]
Promise.all(a)
  .then(v => { console.log(v) })
  .catch(err => { console.error(err) })

const s = new Set([
  new Promise((resolve, reject) => { setTimeout(resolve, 300, 1) }),
  new Promise((resolve, reject) => { setTimeout(resolve, 100, 2) }),
  new Promise((resolve, reject) => { setTimeout(reject, 200, 3) }),
])
Promise.race(s)
  .then(v => { console.log(v) })
  .catch(err => { console.error(err) })
```
<br>

### 6. `generator - yield*` 문법으로 이용 가능

```js
const arr = [1, 2, 3]
const map = new Map([['a', 1], ['b', 2], ['c', 3]])
const set = new Set([1, 2, 3])
const str = '이런것도 된다.'

const makeGenerator = iterable => function* () {
  yield* iterable
}
const arrGen = makeGenerator(arr)()
const mapGen = makeGenerator(map)()
const setGen = makeGenerator(set)()
const strGen = makeGenerator(str)()

console.log(arrGen.next())
console.log(mapGen.next())
console.log(...setGen)
console.log(...strGen)
```

> 여기까지 모두 내부적으로는
> `Symbol.iterator` 또는 `generator`을 실행하여 iterator로 변환한 상태에서
> `next()`를 반복 호출하는 동일한 로직을 기반으로 함.

<br>

### 7. iterable 객체에 `[Symbol.iterator]`가 **잘** 정의되지 않은 경우

```js
const obj = {
  a: 1,
  b: 2,
  [Symbol.iterator] () {
    return 1
  }
}
console.log([...obj])
```

<br>

### 3️⃣ iterable한 개체를 인자로 받을 수 있는 개체

```js
new Map()
new Set()
new WeakMap()
new WeakSet()
Promise.all()
Promise.race()
Array.from()
```

<br><br>

## Iterator

반복을 위해 설계된 특별한 인터페이스를 가진 객체

- 객체 내부에는 `next()` 메소드가 있다.
- 이 메소드는 `value`와 `done` 프로퍼티를 지닌 객체를 반환한다.
- `done` 프로퍼티는 boolean값이다.

<br>

초간단 이터레이터 예시

```js
const iter = {
  items: [10, 20, 30],
  count: 0,
  next () {
	const done = this.count >= this.items.length
    return {
      done,
      value: !done ? this.items[this.count++] : undefined
    }
  }
}
console.log(iter.next())
console.log(iter.next())
console.log(iter.next())
console.log(iter.next())
console.log(iter.next())
```

<br>

### 1️⃣ `iterator` 구현해보기

### 1. 객체에는 'next' 메소드가 존재해야 한다.

```js
const iter = {
  next () {}
}
```
<br>

### 2. next 메소드는 다시 객체를 반환해야 한다.

```js
const iter = {
  next () {
    return {}
  }
}
```
<br>

### 3. 반환되는 객체에는 boolean 값을 가지는 done 프로퍼티가 존재해야 한다.

```js
const iter = {
  next () {
	return {
      done: false
    }
  }
}
console.log(iter.next())
```
<br>

### 4. value 프로퍼티를 추가하고, 일정시점에 done을 true로 변환할 수 있게끔 한다.

```js
const iter = {
  val: 0,
  next () {
    const isDone = ++this.val >= 5
    return {
      done: isDone,
      value: !isDone ? this.val : undefined
    }
  }
}
console.log(iter.next())
```
<br>

### 2️⃣ 기본 이터레이터

* 기본 이터레이터에 접근하기
  * Symbol.iterator를 실행하면 됨

```js
const arr = [ 1, 2 ]
const arrIterator = arr[Symbol.iterator]()
console.log(arrIterator.next())
console.log(arrIterator.next())
console.log(arrIterator.next())
```

* 객체가 이터러블한지 확인하기
  * Symbol.iterator가 있는가? 함수로 되어있는가? 
    
```js
const isIterable = target => typeof target[Symbol.iterator] === 'function'
```
<br>

### 3️⃣ 이터러블한 개체 만들기

### 1. 개체의 Symbol.iterator 메소드를 호출하면 iterator가 반환되도록 한다.

> `for...of`, `...(spread)` 등은 모두 개체 내부 (또는 개체의 `__proto__`)의 [Symbol.iterator]를 실행한 결과를 바탕으로, `done`이 `true`가 될 때까지 계속하여 `next()`를 호출하는 식으로 구현되어 있다.

```js
// 절대 실행하지 말 것!!
const createIterator = () => {
  return {
    next () {
      return {
        done: false
      }
    }
  }
}
const obj = {
  [Symbol.iterator]: createIterator
}
console.log(...obj)
```

```js
// 절대 실행하지 말 것!!
const obj = {
  [Symbol.iterator]() {
    return this
  },
  next() {
    return {
      done: false
    }
  }
}
console.log(...obj)
```
<br>

### 2. done이 true가 나오지 않는 한 이터레이트시 무한정 반복실행한다. 따라서 적절한 시점에 done을 true로 바꾸어주어야 한다.

```js
const createIterator = () => {
  let count = 0
  return {
    next () {
      return {
        done: count > 3
      }
    }
  }
}
const obj = {
  [Symbol.iterator]: createIterator
}
console.log(...obj)
```
<br>

### 3. value 프로퍼티를 추가하면 완성!

```js
const createIterator = function () {
  let count = 0
  const items = Object.entries(this)
  return {
    next () {
      return {
        done: count >= items.length,
        value: items[count++]
      }
    }
  }
}
const obj = {
  a: 1,
  b: 2,
  c: 3,
  d: 4,
  [Symbol.iterator]: createIterator
}
console.log(...obj)
```
<br>

### 4. 객체 내부에 직접 할당한 형태

```js
const obj = {
  a: 1,
  b: 2,
  c: 3,
  d: 4,
  [Symbol.iterator] () {
    let count = 0
    const items = Object.entries(this)
    return {
      next () {
        return {
          done: count >= items.length,
          value: items[count++]
        }
      }
    }
  }
}
console.log(...obj)
```
<br>

### 5. 또는 generator를 실행한 결과 역시 이터러블하다.

```js
const obj = {
  a: 1,
  b: 2,
  c: 3,
  d: 4,
  *[Symbol.iterator] () {
    yield* Object.entries(this)
  }
}
console.log(...obj)
```
<br>

### 6. 정리

- `for-of`, `...(spread operator)`, `forEach 메소드` 등은 내부적으로
- `[Symbol.iterator]`를 실행한 결과 객체를 들고,
- 객체 내부의 `next()` 메소드를
- `done 프로퍼티`가 `true`가 나올 때까지 반복하여 호출한다.
- 즉, Symbol.iterator 메소드의 내용을 위 요구사항에 맞추어 구현하기만 하면 iterable한 객체이다.

> Duck type Protocol : [덕타이핑](https://ko.wikipedia.org/wiki/%EB%8D%95_%ED%83%80%EC%9D%B4%ED%95%91) <br>
> <em>'정해놓은 규칙들만 따르면, 오리라고 간주하겠다'</em>
