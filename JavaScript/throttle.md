# throttle

## 개념

마지막 함수가 호출된 후 일정 시간이 지나기 전에 다시 호출되지 않도록 하는 기법    
**일정 시간에 한 번씩**만 실행되도록 제한을 두는 것

* 스크롤 이벤트에 주로 사용
* 성능 이슈 때문에 많이 사용
    * 특성 자체가 실행 횟수에 제한을 거는 것이기 때문

<br><br>

## 구현

* 타이머가 설정되어 있으면 아무 동작도 하지 않음
* 타이머가 없다면 타이머를 설정
* 타이머는 일정 시간 후에 스스로를 해제하고, ajax 요청 하면 됨

```js
let timer;
document.querySelector('#input').addEventListener('input', function (e) {
    if (!timer) {
        timer = setTimeout(function () {
            timer = null;
            console.log('여기에 ajax 요청', e.target.value);
        }, 200);
    }
});
```

<br>

### 예시

> ⏰ 처음 호출된 후에 지정된 시간 동안 추가 호출을 허용하지 않음

```js
const throttle = (callback, ms) => {
    let timer; // 나중에 쓰로틀링된 함수가 실행될 때 사용됨, null 또는 undefined인 경우에만 함수가 실행

    return (...args) => { // 인자로 ...args를 받아 나중에 실행될 callback 함수에 전달
        if (!timer) { // 쓰로틀링된 함수가 이미 예정된 상태에서 호출되었을 때 중복 실행되지 않도록 함 
            timer = setTimeout(() => { // 주어진 시간(ms) 이후에 내부 콜백 함수를 실행
                timer = null; // timer 변수를 null로 설정하여 다음 호출을 위해 초기화
                callback(...args); // 콜백 함수 실행 
            }, ms);
        }
    }
};

const handleThrottle = throttle(handleResize, 1000); // React의 경우 useCallback 사용 가능 
```

* callback : 실행을 제한하려는 함수, 쓰로틀링되어 실행됨
* ms : 쓰로틀링 간격을 나타내는 시간(ms), 이 시간 간격 내에 중복 실행되지 않도록 함

<br><br>

## 참고 사이트

> https://www.zerocho.com/category/JavaScript/post/59a8e9cb15ac0000182794fa  
> https://inpa.tistory.com/entry/jQuery-%F0%9F%93%9A-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-resize-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EC%82%AC%EC%9A%A9%EB%B2%95-%EC%B5%9C%EC%A0%81%ED%99%94
