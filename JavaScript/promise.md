# Promise

## 소개

### Callback Hell

- id가 'btn'인 button을 클릭하면 서버에 users 리스트를 가져오는 요청을 하고,
- 성공하면 list의 세번째 user의 정보를 다시 요청하여
- 성공하면 user의 profileImage url값을 가져다가 image 태그로 표현하고,
- 이 image를 클릭하면 해당 이미지를 제거.

```js
const script= document.createElement('script')
script.src= 'https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.min.js'
document.body.appendChild(script)

document.body.innerHTML += '<button id="btn">클릭</button>'
document.getElementById('btn').addEventListener('click', function (e) {
  $.ajax({
    method: 'GET',
    url: 'https://api.github.com/users?since=1000',
    success: function (data) {
      var target = data[2]
      $.ajax({
        method: 'GET',
        url: 'https://api.github.com/user/' + target.id,
        success: function (data) {
          var _id = 'img' + data.id
          document.body.innerHTML += '<img id="' + _id + '" src="' + data.avatar_url + '"/>'
          document.getElementById(_id).addEventListener('click', function (e) {
            this.remove()
          })
        },
        error: function (err) {
          console.error(err)
        }
      })
    },
    error: function (err) {
      console.error(err)
    }
  })
})
```

<br>

### Promise

```js
document.body.innerHTML = '<button id="btn">클릭</button>'
document.getElementById('btn').addEventListener('click', function (e) {
    fetch('https://api.github.com/users?since=1000')
    .then(function (res) { return res.json() })
    .then(function (res) {
        var target = res[2]
        return fetch('https://api.github.com/user/' + target.id)
    })
    .then(function (res) { return res.json() })
    .then(function (res) {
        var _id = 'img' + res.id
        document.body.innerHTML += '<img id="' + _id + '" src="' + res.avatar_url + '"/>'
        document.getElementById(_id).addEventListener('click', function (e) {
            this.remove()
        })
    })
    .catch(function (err) {
        console.error(err)
    })
})
```
* 간결하고 가독성이 높아짐

<br>

### Promise를 반환하면서 JSON parsing을 자동으로 해주는 library (axios) 활용시

```js
const script= document.createElement('script')
script.src= 'https://cdnjs.cloudflare.com/ajax/libs/axios/0.18.0/axios.min.js'
document.body.appendChild(script)

document.body.innerHTML += '<button id="btn">클릭</button>'
document.getElementById('btn').addEventListener('click', function (e) {
    axios.get('https://api.github.com/users?since=1000')
    .then(function (res) {
        var target = res.data[2]
        return axios.get('https://api.github.com/user/' + target.id)
    })
    .then(function (res) {
        var _id = 'img' + res.data.id
        document.body.innerHTML += '<img id="' + _id + '" src="' + res.data.avatar_url + '"/>'
        document.getElementById(_id).addEventListener('click', function (e) {
            this.remove()
        })
    })
    .catch(function (err) {
        console.error(err)
    })
})
```
<br>

## 상세

### Promise Status

- unnsettled (미확정) 상태: pending. thenable하지 않다. (비동기 처리가 끝나기 전)
- settled (확정) 상태: resolved. thenable한 상태.
   - fulfilled (성공)
   - rejected (실패)

```js
const promiseTest = param => new Promise((resolve, reject) => {
	setTimeout(() => {
		if (param) {
			resolve("해결 완료")
		} else {
			reject(Error("실패!!"))
		}
	}, 1000)
})

const testRun = param => promiseTest(param)
  .then(text => { console.log(text) })
  .catch(error => { console.error(error) })

const a = testRun(true)
const b = testRun(false)
```
* 비동기 처리를 할 수 있게 해줌
* resolved는 확정상태 자체 또는 성공 표시 둘 중 하나로 쓰이기 때문에, 문맥에 따라서 파악해야 한다. 

<br>

### 문법

- `new Promise(function)`
- `.then()`, `.catch()`는 언제나 promise를 반환한다.

```js
const executer = (resolve, reject) => { ... }
const prom = new Promise(executer)

const onResolve = res => { ... }
const onReject = err => { ... }

// (1)
prom.then(onResolve, onReject)

// (2)
prom.then(onResolve).catch(onReject)
```

```js
new Promise((resolve, reject) => { ... })
.then(res => { ... })
.catch(err => { ... })
```
* 일반적으로 사용하는 방법

```js
const simplePromiseBuilder = value => {
  return new Promise((resolve, reject) => {
    if(value) { resolve(value) }
    else { reject(value) }
  })
}

simplePromiseBuilder(1)
  .then(res => { console.log(res) })
  .catch(err => { console.error(err) })

simplePromiseBuilder(0)
  .then(res => { console.log(res) })
  .catch(err => { console.error(err) })
```

```js
const simplePromiseBuilder2 = value => {
  return new Promise((resolve, reject) => {
    if(value) { resolve(value) }
    else { reject(value) }
  })
  .then(res => { console.log(res) })
  .catch(err => { console.error(err) })
}

simplePromiseBuilder2(1)
simplePromiseBuilder2(0)
```
* 중복 제거

```js
const prom = new Promise((resolve, reject) => {
  resolve()
  reject()
  console.log('Promise')
})
prom.then(() => {
  console.log('then')
})

prom.catch(() => {
  console.log('catch')
})

console.log('Hi!')
```

```js
const prom = new Promise((resolve, reject) => {
  reject()
  resolve()
  console.log('Promise')
})
prom.then(() => {
  console.log('then')
})

prom.catch(() => {
  console.log('catch')
})

console.log('Hi!')
```
1. then이나 catch 구문은 실행큐에 후순위로 등록되고 실행된다.
2. promise 인스턴스에 넘긴 함수 내부에서는, resolve나 reject 둘 중에 먼저 호출된 것만 실제로 실행된다.
3. 사실은 실제로 실행되는 것이 아니라, (실행은 둘 다 된다) pending 상태일 때만 의미가 있기 때문에 2번 결과가 나온 것

<br>

### 확장 Promise 만들기

1. `Promise.resolve`, `Promise.reject`

```js
Promise.resolve(42)
.then(res => { console.log(res) })
.catch(err => { console.error(err) })

Promise.reject(12)
.then(res => { console.log(res) })
.catch(err => { console.error(err) })
```
<br>

2. thenable 객체

```js
const thenable = {
  then (resolve, reject) {
    resolve(33)
  }
}
const prom = Promise.resolve(thenable)
prom.then(res => { console.log(res) })
```

```js
const thenable = {
  then (resolve, reject) {
    reject(33)
  }
}
const prom = Promise.resolve(thenable)
prom.catch(err => { console.log(err) })
```
* thenable : 앞의 것이 끝나면 이어서 할 수 있는
* promise에서 반환된 것들은 전부 thenable하다.
* then 메소드가 있으면 thenable하다.

<br>

### ⭐️Promise Chaning (then, catch에서 return)

```js
new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('첫번째 프라미스')
  }, 1000)
}).then(res => {
  console.log(res)
  return '두번째 프라미스'
}).then(res => {
  console.log(res)  //두번째 프라미스
  return new Promise((resolve, reject) => {
    setTimeout(() => {
          resolve('세번째 프라미스')
    }, 1000)
  })
}).then(res => {
  console.log(res)  //세번째 프라미스
  return new Promise((resolve, reject) => {
    setTimeout(() => {
          reject('네번째 프라미스')
    }, 1000)
  })
}).then(res => {
  console.log(res)  //무시하고 넘어감
}).catch(err => {
  console.error(err)
  return new Error('이 에러는 then에 잡힙니다.')
}).then(res => {
  console.log(res)  //이 에러는 then에 잡힙니다.
  throw new Error('이 에러는 catch에 잡힙니다.')
}).then(res => {
  console.log('출력 안됨')  //건너뜀
}).catch(err => {
  console.error(err)
})
```
****.then이나 .catch 안에서****

  1. return promise 인스턴스 : promise 인스턴스가 리턴된 것
     * = return new Promise() or return Promise.resolve()  
  2. return 일반값 : promise 객체에 resolved 상태로 반환됨. 그 안에 값이 담김
     * Promise {<< resolved >>: 값} 
  3. return 안하면 : return undefined (원래 JS 동작) -> 2번과 같음
  4. Promise.resolve() or Promise.reject() : return 해주지 않는 이상 의미 없음
     * 별개의 프라미스 객체가 생성될 뿐, 현재 process상의 Promise 플로우에 영향주지 않음. 
     * return한 것은 1번과 같음


<br>

### Error Handling

```js
asyncThing1()
.then(asyncThing2)
.then(asyncThing3)
.catch(asyncRecovery1)
.then(asyncThing4, asyncRecovery2)  //asyncThing4가 실패하면 다음번 catch로 감
.catch(err => { console.log("Don't worry about it") })
.then(() => { console.log("All done!") })
```

![에러 핸들링](https://raw.githubusercontent.com/js-jsm/es6js/master/15%20%ED%94%84%EB%9D%BC%EB%AF%B8%EC%8A%A4/promise_chaining.png)

<br>

### Multi Handling

#### 1. `Promise.all()`

- iterable의 모든 요소가 fulfilled되는 경우: 전체 결과값들을 배열 형태로 then에 전달.
- iterable의 요소 중 일부가 rejected되는 경우: 가장 먼저 rejected 되는 요소 '하나'의 결과를 catch에 전달.

```js
const arr = [
	1,
	new Promise((resolve, reject) => {
		setTimeout(()=> {
			resolve('resolved after 1000ms')
		}, 1000)
	}),
	'abc',
	() => 'not called function',
	(() => 'IIFE')()
]

Promise.all(arr)  //모든게 실행된 후
.then(res => { console.log(res) })
.catch(err => { console.error(err) })
```

****Promise.all(iterable)**** <br>
Array.prototype.every()와 비슷

1. 일반값은 그냥 resolved된 값으로 간주
2. iterable 내의 모든 요소들이 resolved된 순간에 다음번 then 호출. 이때 값은 iterable 실행 결과가 배열로 반환됨
3. iterable 내의 일부 요소가 하나라도 reject되면, 그 순간 catch를 호출하며, reject된 값만 넘어온다.

<br>

`All` or `one error`


```js
const arr = [
	1,
	new Promise((resolve, reject) => {
		setTimeout(()=> {
			reject('rejected after 1000ms')
		}, 1000)
	}),
	'abc',
	()=> 'not called function',
	(()=> 'IIFE')()
]

Promise.all(arr)
.then(res => { console.log(res) })
.catch(err => { console.error(err) })
```
<br>

#### 2. `Promise.race()`

- iterable의 요소 중 가장 먼저 fulfilled / rejected되는 요소의 결과를 then / catch에 전달.

```js
const arr = [
	new Promise(resolve => {
		setTimeout(()=> { resolve('1번요소, 1000ms') }, 1000)
	}),
	new Promise(resolve => {
		setTimeout(()=> { resolve('2번요소, 500ms') }, 500)
	}),
	new Promise(resolve => {
		setTimeout(()=> { resolve('3번요소, 750ms') }, 750)
	})
]
Promise.race(arr)
.then(res => { console.log(res) })
.catch(err => { console.error(err) })
```
****Promise.race(iterable)**** <br>
Array.prototype.some()과 비슷

1. 일반값은 그냥 resolved된 값으로 간주
2. iterable 내의 요소 중에 가장 먼저 resolved (then) 또는 rejected (catch)된 값을 반환함

`only the fastest one`

```js
const arr = [
	new Promise(resolve => {
		setTimeout(()=> { resolve('1번요소, 0ms') }, 0)
	}),
	'no queue'
]
Promise.race(arr)
.then(res => { console.log(res) })
.catch(err => { console.error(err) })
```
<br>

> 참고: [ES2017 Async Function](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/async_function)
* await를 쓰면 비동기로 간주