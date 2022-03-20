# set, weakset

## Set

```js
Array.prototype.pushUnique = value => {
  if(!this.includes(value)) {
    this.push(value)
  }
  return this
}
const arr = [1, 2, 3]
arr.pushUnique(5)
arr.pushUnique(4)
arr.pushUnique(3)
```

```js
const set = new Set([1, 2, 3])
set.add(5)
set.add(4)
set.add(3)
```

<br>

### 1. 중복이 허용되지 않으며 순서를 보장하는, 값들로만 이루어진 리스트

<br>

### 2. 추가, 삭제, 초기화, 요소의 총 개수, 포함여부확인

```js
const set = new Set()
set.add(5)
set.add('5')
set.add(-0)
set.add(+0)

console.log(set.size)  //3 

console.log(set.has(5))  //true 포함여부 확인
console.log(set.has(6))  //false

set.delete(5)
console.log(set.has(5))  //false

set.clear()  //전부 삭제
console.log(set.size)  //0
console.log(set)
```
* 배열에서의 삭제는 index를 알아야 함
* set은 index 개념이 없음 (순서는 보장된다)

<br>

### 3. 초기값 지정

인자로 iterable한 개체를 지정할 수 있다.

```js
const set1 = new Set([1, 2, 3, 4, 5, 3, 4, 2])
console.log(set1)

const map = new Map()
map.set('a', 1).set('b', 2).set({}, 3)
const set2 = new Set(map)  //() 안에 iterable한 어떤 객체가 와도 상관 없다 
console.log(set2)

const gen = function* () {
	for (let i = 0; i < 5; i++) {
		yield i+1
  }
}
const set = new Set(gen())
```
* 초기값을 지정할 때는 배열로 넣을 수 있다
* iterable 하다, 펼칠 수 있다
* iterable object : array, string, map, set

<br>

### 4. 인덱스(키)가 없다!

```js
console.log(set.keys())
console.log(set.values())
console.log(set.entries())

console.log(...set.keys())  //셋 다 동일
console.log(...set.values())
console.log(...set.entries())

set.forEach(function(key, value, ownerSet) {
  console.log(key, value, this)
}, {})

console.log(set[1])
```
* 중복을 무시한다
* key = value
* 더 빨리 순회 가능
* 인덱스 값을 모를 때 유용

<br>

### 5. 배열로 전환하기

```js
const set = new Set([1, 2, 3, 3, 4, 4, 5, 5, 1])
const arr = [...set]
console.log(arr)
```
<br>

### 6. 중복 제거한 배열 만들기

```js
const makeUniqueArray = arr => [...new Set(arr)]
const arr = [1, 2, 3, 3, 4, 4, 5, 5, 1]

const newArr = makeUniqueArray(arr)
console.log(newArr)
```

#### set이 배열보다 효과적인 경우
1. 배열의 중복을 제거하고 다시 새로운 배열을 만들 때
2. 전체순회할 필요성이 있는 경우
3. 값의 유무 판단

<br>

#### 좋지 않은 경우
1. 특정 요소에 접근
2. 인덱스가 필요한 경우

<br><br>

## WeakSet

### 1. set과의 비교

set에 객체를 저장할 경우 set에도 해당 객체에 대한 참조가 연결되어, 여타의 참조가 없어지더라도 set에는 객체가 여전히 살아있음.  
한편 WeakSet은 객체에 대한 참조카운트를 올리지 않아, 여타의 참조가 없어질 경우 WeakSet 내의 객체는 G.C의 대상이 됨.

```js
const obj1 = { a: 1 }
const set = new Set()
set.add(obj1)
obj1 = null
```

```js
const obj2 = { b: 2 }
const wset = new WeakSet()
wset.add(obj2)
obj2 = null
```
* 참조카운트를 증가시키지 않음 

    ```js
    const s = new WeakSet()  // 참조카운트 증가시키지 않음
    
    let o = {};  // o라는 변수가 {} 객체를 참조 -> 참조카운트 1
    let o2 = o;  // o2라는 변수도 o를 통해서 {} 객체를 참조 -> 참조카운트 2
    
    /*    
    o2 = null;  // o2에 null이 들어가서 -> {} 객체의 참조카운트는 1
    o = null;  // {} 참조카운트 0 -> Garbage Collector의 수거 대상이 된다. -> GC되면 s에는 아무것도 없게 된다
    */
  
    s.add(o);  // o라는 변수가 가르키는 {}를 s에 추가했지만, 참조카운트는 여전히 1
    ```

<br>

### 2. 참조형 데이터만 요소로 삼을 수 있다.
<br>

### 3. iterable이 아니다.
- for ... of 사용 불가
- size 프로퍼티 없음
- `wset.keys()`, `wset.values()`, `wset.entries()` 등 사용 불가

<br>

### 4. 활용사례는 아직까지는 많지 않다.

- [use case of WeakSet](https://www.sitepoint.com/using-the-new-es6-collections-map-set-weakmap-weakset/) (알려진건 하나뿐..)

```js
const isMarked = new WeakSet()
const attachedData = new WeakMap()

class Node {
  constructor (id) {
    this.id = id
  }
  mark () { isMarked.add(this) }
  unmark () { isMarked.delete(this) }
  set data (data) { attachedData.set(this, data) }
  get data () { return attachedData.get(this) }
}

let foo = new Node('foo')
foo.mark()
foo.data = 'bar'
console.log(foo.data)

isMarked.has(foo)
attachedData.has(foo)

foo = null

// G.C 수거해간 이후..
isMarked.has(foo)
attachedData.has(foo)
```
* has는 가능
