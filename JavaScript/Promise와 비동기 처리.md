# Promise와 비동기 처리

## Promise

Promise 객체 : 비동기 작업이 맞이할 미래의 완료 또는 실패와 그 결과 값

### Promise의 상태

* 대기(pending): 이행하지도, 거부하지도 않은 초기 상태
* 이행(fulfilled): 연산이 성공적으로 완료됨
* 거부(rejected): 연산이 실패함

### 인스턴스 메서드

1. `Promise.prototype.catch()`     
오류 처리   
프로미스에 거부 처리기 콜백을 추가하고, 콜백이 호출될 경우 그 반환값으로 이행하며 호출되지 않을 경우,   
즉 이전 프로미스가 이행하는 경우 이행한 값을 그대로 사용해 이행하는 새로운 프로미스를 반환

2. `Promise.prototype.then()`  
성공적으로 받아온 요청의 결과값  
프로미스에 이행과 거부 처리기 콜백을 추가하고, 콜백이 호출될 경우 그 반환값으로 이행하며   
호출되지 않을 경우(onFulfilled, onRejected 중 상태에 맞는 콜백이 함수가 아닐 경우)   
처리된 값과 상태 그대로 처리되는 새로운 프로미스를 반환

3. `Promise.prototype.finally()`  
프로미스의 이행과 거부 여부에 상관없이 처리될 경우 항상 호출되는 처리기 콜백을 추가하고, 이행한 값 그대로 이행하는 새로운 프로미스를 반환


<br><br>

## async/await 

`async`와 `await` 문법을 사용하면 Promise를 좀 더 편하게 사용할 수 있음  
비동기 코드를 동기적으로 보이도록 작성할 수 있어 간단하고 가독성이 좋음  

<br><br>

## 예시

### async/await 사용 

```ts
const handleClickSignIn = async () => {
    if (!isDisabledSubmit) {
        try {
            const response = await http.post('/user/signin', {
                email: user.email,
                password: user.password,
            });
            const accessToken = response.data.user.user_token;
            localStorage.setItem('ACCESS_TOKEN', JSON.stringify(accessToken));
            navigate(PATH.CALENDAR);
        } catch (e) {
            const error = handleAxiosError(e);
            alert(error.msg);
        }
    }
};
```

### Promise then catch 사용

```ts
const handleClickSignIn = () => {
    if (!isDisabledSubmit) {
        const response = http.post('/user/signin', {
            email: user.email,
            password: user.password,
        });
        response.then((response) => {
            const accessToken = response.data.user.user_token;
            localStorage.setItem('ACCESS_TOKEN', JSON.stringify(accessToken));
            navigate(PATH.CALENDAR);
        }).catch ((e) => {
            const error = handleAxiosError(e);
            alert(error.msg);
        })
    }
};
```

<br><br>

## 참고 사이트

> https://ko.javascript.info/promise-basics  
> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise
