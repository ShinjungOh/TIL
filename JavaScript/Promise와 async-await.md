# Promise와 async/await

## Promise

### 1. promise 객체 생성하기 

```tsx
const promise = new Promise(function(resolve, reject) {
  // executor (실행자, 실행 함수)
   // 대개 시간이 걸리는 일을 수행
});
```

#### promise 객체의 내부 프로퍼티

* `state` : 처음엔 `pending`(보류)였다가 resolve가 호출되면 `fulfilled`, reject가 호출되면 `rejected`로 변화 
* `result` : 처음엔 `undefined`였다가 resolve(value)가 호출되면 `value`로, reject(error)가 호출되면 `error`로 변화

<br>

### 2. 실행 함수 executor  

executor는 자동으로 실행되는데 여기서 원하는 작업이 처리됨  
처리가 끝나면 executor는 처리 **성공 여부에 따라** `resolve`나 `reject`를 호출

![](../Images/프로미스_프로퍼티.png)

1. executor의 인수 `resolve`와 `reject`
   * 자바스크립트에서 **자체 제공하는 콜백**
   * resolve와 reject를 신경 쓰지 않고 **executor 안의 코드**만 작성하면 됨
   * executor에선 결과를 즉시 얻든 늦게 얻든 상관없이, 인수로 넘겨준 콜백 중 **하나를 반드시 호출**해야 함 

2. 결과 
   * `resolve(value)` : 일이 **성공**적으로 끝난 경우 그 결과를 나타내는 `value`와 함께 호출 
   * `reject(error)` : **에러** 발생 시 에러 객체를 나타내는 `error`와 함께 호출
   
3. 주의점
   * executor는 resolve나 reject 중 **하나를 반드시 호출**해야 함
   * 변경된 상태는 더 이상 변하지 않음 - 처리가 끝난 프로미스에 resolve와 reject를 호출하면 무시됨 

<br>

### 3. 소비 함수와 then, catch, finally 메소드 

#### 📍 then

```
.then(promise가 이행되었을 때 실행되는 함수(실행 결과를 받음), promise가 거부되었을 때 실행되는 함수(에러를 받음)) 
```

```js
promise.then(
  function(result) { /* 결과(result)를 다룸 */ },
  function(error) { /* 에러(error)를 다룸 */ }
);
```   

#### 📍 catch

에러가 발생한 경우만 다루고 싶을 때

* `.then(null, errorHandlingFunction)` : null을 첫 번째 인수로 전달하기
* `.catch(errorHandlingFunction)`

> .catch(f)는 문법이 간결하다는 점만 빼고 .then(null,f)과 완벽하게 같음 

```js
promise.catch(alert); // 1초 뒤 "Error: 에러 발생!" 출력
```

#### 📍 finally

프로미스가 처리되면(resolve 또는 reject) f가 항상 실행된다는 점에서 `.finally(f)` 호출은 `.then(f, f)`과 유사

<br>

### 4. 마이크로태스크 큐

> 프로미스 핸들러 `.then/catch/finally`는 항상 **비동기적**으로 실행     
> 즉시 실행되는 프로미스이더라도 `.then/catch/finally` 아래에 있는 코드는 이 핸들러가 **실행되기 전에** 실행

비동기 작업을 처리하려면 관리가 필요  
💡 `PromiseJobs라는 내부 큐(internal queue)` 또는 `마이크로태스크 큐(microtask queue)`(V8 엔진에서) 라고 부름   
**프로미스 핸들러는 항상 마이크로태스크 큐를 통과함**

![](../Images/프로미스_마이크로태스크.png)

* 마이크로태스크 큐는 먼저 들어온 작업을 먼저 실행(FIFO, first-in-first-out)
* 실행할 것이 **아무것도 남아있지 않을 때만** 마이크로태스크 큐에 있는 작업이 실행되기 시작

#### 실행 순서가 중요한 경우엔 .then을 사용해 큐에 넣으면 됨 

```js
Promise.resolve()
        .then(() => alert("프라미스 성공!"))
        .then(() => alert("코드 종료"));
```

<br>

### 예제

프로미스를 기반으로 하는 동일 기능 함수  
함수 delay(ms)는 프로미스를 반환하고, 반환되는 프로미스는 .then을 붙일 수 있도록 ms 이후에 이행됨

```js
function delay(ms) {
    new Promise((resolve) => {
        setTimeout(resolve, ms)
    });
}

delay(3000).then(() => alert('3초후 실행'));
```

<br><br>

## async/await

Promise를 핸들링하는 또 다른 문법 await  
읽고 쓰기 쉬운 비동기 코드를 작성할 수 있음  
await는 promise.then보다 좀 더 세련되게 Promise의 result 값을 얻을 수 있도록 해주는 문법

> 📌 **async/await의 흐름**
> 
> 함수를 호출하고, 함수 본문이 실행되는 도중에 `await` 키워드를 만나면    
> 함수 실행이 잠시 **중단**되었다가 Promise가 처리될 때까지 **대기**(await = 기다리다)  
> Promise가 처리되면 함수 실행이 재개되며 **결과 반환** -> Promise 객체의 result 값이 변수 result 등에 할당됨    
> Promise가 처리되길 기다리는 동안 엔진이 다른 일(다른 스크립트를 실행, 이벤트 처리 등)을 할 수 있어서, CPU 리소스가 낭비되지 않음

<br>

### 특징  

* async가 붙은 함수는 **반드시 Promise를 반환** 
  * Promise가 아닌 것은 프라미스로 감싸 반환
* await는 async 함수 안에서만 동작
  * 일반 함수엔 await을 사용할 수 없음 
* await는 최상위 레벨 코드에서 작동하지 않음
  * 익명 async 함수로 코드를 감싸면 최상위 레벨 코드에도 await를 사용할 수 있음

<br>

### async/await와 promise.then/catch

async/await를 사용하면 promise.then/catch가 거의 필요 없음  

💡 **가장 바깥 스코프에서 비동기 처리가 필요할 때** 같이 `promise.then/catch`를 써야만 하는 경우가 있음  
-> async/await가 Promise를 기반으로 한다는 사실을 알고 있어야 함   
여러 작업이 모두 완료될 때까지 기다리려면 `Promise.all`을 활용할 수 있음 

<br>

### thenable

thenable = then 메소드가 있음

await는 ‘thenable’ 객체를 받음 
promise.then처럼 await에도 thenable 객체(then 메서드가 있는 호출 가능한 객체)를 사용할 수 있음  
thenable 객체는 서드파티 객체가 프라미스가 아니지만 프라미스와 호환 가능한 객체를 제공할 수 있다는 점에서 생긴 기능  
서드파티에서 받은 객체가 .then을 지원하면 이 객체를 await와 함께 사용할 수 있음 

<br>

### 에러 핸들링

await가 던진 에러는 throw가 던진 에러를 잡을 때처럼 `try..catch`를 사용해 잡을 수 있음

* 프로미스가 정상적으로 이행 시 : await promise는 프로미스 객체의 result에 저장된 값을 반환
* 프로미스가 거부 시 : throw문을 작성한 것처럼 에러가 던져짐 

예시:

```js
try {
    // ...
} catch (e) {
   // ...
}
```

<br><br>

## 예시 - 모달 OverlayProvider에서의 Promise 

* Promise가 성공했을 때의 결과를 원하는 시점에 호출하기 위해 Promise 사용
* async/await를 사용하면 await는 async 함수 안에서만 동작하며, 코드가 동기적인 형태로 작성되기 때문에 사용하지 않은 것 

```tsx

export const OverlayProvider = ({children}: PropsWithChildren) => {
    const [overlay, setOverlay] = useState<OverlayState | null>(null);

    const openOverlay: OverlayOpenFn = useCallback((children, option) => {
        if (isValidElement(children)) {
            setOverlay({
                content: children,
                options: {...defaultOverlayClickOption, ...(option ?? {})},
            });

            return new Promise((resolver) => {
                console.log('Promise 객체 생성됨');
                // resolver(1); -> 1이 반환되며 프로미스 처리가 완료, 이후에 resolve와 reject를 호출하면 무시됨  
                setOverlay((prevOverlay) => (prevOverlay ? {...prevOverlay, resolver} : prevOverlay));
            }); // 모달이 켜졌을 때 여기까지 진행된 상태
        }

        return null;
    }, []);

    const handleSubmitOverlay = (result: OverlaySubmitResult) => {
        console.log('제출');
        overlay?.resolver?.(result); // -> resolve() 를 value와 함께 호출하며 Promise가 종료
        console.log('Promise가 끝남!');
        handleCloseOverlay();
    };
    
    // return (...)
}
```

* useOverlay의 반환값으로는 `resolver(value)`를 실행하면서 넘겨준 값이 담김

<br>

### async/await와 비교 

```tsx
const getItem = async () => {
  const response = await http.get(); // response가 resolver랑 같음, 실행결과가 아니라 실행할 수 있는 무언가
  return response; // 반환값 
}

getItem();
```

<br>

### 옵셔널 체이닝

1과 2는 동일한 로직

```tsx
// 1.
overlay?.resolver?.(result);

// 2. 
if (overlay) {
    if (overlay.resolver) {
        overlay.resolver(result);  // await http.get()가 성공했다는 가정과 같음 // return response과 같음
    }
}
```

<br><br>

## 참고 사이트

> https://ko.javascript.info/promise-basics  
> https://ko.javascript.info/async-await  
> https://ko.javascript.info/event-loop     
> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve
