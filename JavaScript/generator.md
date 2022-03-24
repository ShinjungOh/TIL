# Generator

## 소개

- 중간에서 멈췄다가 이어서 실행할 수 있는 함수 
- function 키워드 뒤에 `*`를 붙여 표현하며, 함수 내부에는 `yield` 키워드를 활용한다. (yield: 넘겨주다, 양도하다 -> 함수 밖으로 값을 넘겨준다)
- 함수 실행 결과에 대해 `next()` 메소드를 호출할 때마다 순차적으로 제너레이터 함수 내부의 `yield` 키워드를 만나기 전까지 실행하고, `yield` 키워드에서 일시정지한다.
- 다시 `next()` 메소드를 호출하면 그 다음 `yield` 키워드를 만날 때까지 함수 내부의 내용을 진행하는 식이다.

```js
function* gene () {
  console.log(1)
  yield 1
  console.log(2)
  yield 2
  console.log(3)
}
const gen = gene()
```

- 선언 방식

```js
function* gene () { yield }
const gene = function* () { yield }
const obj = {
  gene1: function* () { yield }
  *gene2 () { yield }
}
class A {
  *gene () { yield }
}
```
* function 뒤에 `*` 표시 (띄어쓰기 중요x)
* 이름 앞에 `*` 표시

<br>

## 이터레이터로서의 제너레이터

```js
function* gene () {
  console.log(1)
  yield 1
  console.log(2)
  yield 2
  console.log(3)
}
const gen = gene()
console.log(...gen)
```

```js
const obj = {
  a: 1,
  b: 2,
  c: 3,
  *[Symbol.iterator] () {
    for (let prop in this) {
      yield [prop, this[prop]]
    }
  }
}
console.log(...obj)
for (let p of obj) {
  console.log(p)
}
```
<br>

## `yield* [iterable]`

```js
function* gene () {
  yield* [1, 2, 3, 4, 5]
  yield
  yield* 'abcde'
}
for (const c of gene()) {
  console.log(c)
}
```

```js
function* gene1 () {
  yield [1, 10]
  yield [2, 20]
}
function* gene2 () {
  yield [3, 30]
  yield [4, 40]
}
function* gene3 () {
  console.log('yield gene1') // yield* gene1()
  yield* gene1()
  console.log('yield gene2')  // yield* gene2()
  yield* gene2()
  console.log('yield* [[5, 50], [6, 60]]')
  yield* [[5, 50], [6, 60]]
  console.log('yield [7, 70]')
  yield [7, 70]
}
const gen = gene3()
for (let [k, v] of gen) {
  console.log(k, v)
}
```
* generator 중첩해서 사용 가능

<br>

### 인자 전달하기

```js
function* gene () {
  let first = yield 1
  let second = yield first + 2
  yield second + 3
}
const gen = gene()
console.log(gen.next().value)
console.log(gen.next().value)
console.log(gen.next().value)
```
* 작동방법 외우기
* 덕분에 외부와 소통할 수 있다 
* 넘겨준 값으로 다음번 yield에 영향을 줄 수 있다

<br>

### 비동기 작업 수행

```js
const ajaxCalls = () => {
  const res1 = fetch.get('https://api.github.com/users?since=1000')
  const res2 = fetch.get('https://api.github.com/user/1003')
}
const m = ajaxCalls()
```
userId가 1000번 이후인 데이터를 가져와서 그 중 4번째에 위치한 유저 정보를 보려고 하는 경우

<br>

`1`
```js
const fetchWrapper = (gen, url) => fetch(url)
  .then(res => res.json())
  .then(res => gen.next(res));

function* getNthUserInfo() {
  const [gen, from, nth] = yield;
  const req1 = yield fetchWrapper(gen, `https://api.github.com/users?since=${from || 0}`);
  const userId = req1[nth - 1 || 0].id;
  console.log(userId);
  const req2 = yield fetchWrapper(gen, `https://api.github.com/user/${userId}`);
  console.log(req2);
}
const runGenerator = (generator, ...rest) => {
  const gen = generator();
  gen.next();
  gen.next([gen, ...rest]);  //나머지로 넘겨주는 것이 from, nth값이 됨 
}
runGenerator(getNthUserInfo, 1000, 4);
runGenerator(getNthUserInfo, 1000, 6);
```
<br>

`2`
```js
const fetchWrapper = url => fetch(url).then(res => res.json());
function* getNthUserInfo() {
  const [from, nth] = yield;
  const req1 = yield fetchWrapper(`https://api.github.com/users?since=${from || 0}`);
  const userId = req1[nth - 1 || 0].id;
  console.log(userId);
  const req2 = yield fetchWrapper(`https://api.github.com/user/${userId}`);
  console.log(req2);
}
const runGenerator = (generator, ...rest) => {
  const gen = generator();
  gen.next();
  gen.next([...rest]).value
    .then(res => gen.next(res).value)  //promise 구
    .then(res => gen.next(res));
}
runGenerator(getNthUserInfo, 1000, 4);
runGenerator(getNthUserInfo, 1000, 6);
```