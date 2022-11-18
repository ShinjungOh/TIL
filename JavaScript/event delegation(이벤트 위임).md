# event delegation (이벤트 위임)

## 이벤트 위임

다수의 자식 요소에 각각 이벤트 핸들러를 바인딩하는 대신, `하나의 부모 요소`에 이벤트 핸들러를 바인딩하는 방법

<br>

### 사용법

1️⃣ 컨테이너에 하나의 핸들러를 할당  
2️⃣ 핸들러의 `event.target`을 사용해 이벤트가 발생한 요소가 어디인지 찾기  
3️⃣ 원하는 요소에서 이벤트가 발생했다고 확인되면 이벤트를 핸들링  

<br><br>

## 예시 - 이벤트 위임 ❎

```html
<ul id="post-list">
    <li id="post-1">Item 1</li>
    <li id="post-2">Item 2</li>
    <li id="post-3">Item 3</li>
    <li id="post-4">Item 4</li>
    <li id="post-5">Item 5</li>
    <li id="post-6">Item 6</li>
</ul>
```

```js
function printId() {
console.log(this.id);
}

document.querySelector('#post-1').addEventListener('click', printId);
document.querySelector('#post-2').addEventListener('click', printId);
document.querySelector('#post-3').addEventListener('click', printId);
document.querySelector('#post-4').addEventListener('click', printId);
document.querySelector('#post-5').addEventListener('click', printId);
document.querySelector('#post-6').addEventListener('click', printId);
```

모든 li 요소가 클릭 이벤트에 반응하는 처리를 구현하고 싶은 경우,   
li 요소에 이벤트 핸들러를 바인딩하면 총 6개의 이벤트 핸들러를 바인딩해야 함

<br>

### 단점
⚠️ 요소의 갯수만큼 이벤트 핸들러를 바인딩해야 함  
* 실행 속도 저하, 코드가 길어지고 불편   
* 동적으로 요소가 추가되는 경우, 아직 추가되지 않은 요소는 DOM에 존재하지 않으므로 이벤트 핸들러 바인딩 불가

<br><br>

## 예시 - 이벤트 위임 ✅

```js
const msg = document.querySelector('.msg');  // <div class="msg">
const list = document.querySelector('.post-list')  // <ul class="post-list">

list.addEventListener('click', function (e) {
    // 이벤트를 발생시킨 요소
    console.log('[target]: ' + e.target);
    // 이벤트를 발생시킨 요소의 nodeName
    console.log('[target.nodeName]: ' + e.target.nodeName);

    // li 요소 이외의 요소에서 발생한 이벤트는 대응하지 않는다.
    if (e.target && e.target.nodeName === 'LI') {
        msg.innerHTML = 'li#' + e.target.id + ' was clicked!';
    }
});
```

6개의 자식 요소에 각각 이벤트 핸들러를 바인딩하는 것 대신, 부모 요소(ul#post-list)에 이벤트 핸들러를 바인딩  
* DOM 트리에 새로운 li 요소를 추가하더라도 이벤트 처리는 부모 요소인 ul 요소에 위임되었기 때문에 새로운 요소에 이벤트를 핸들러를 다시 바인딩할 필요가 없음 
  * 이벤트가 이벤트 흐름에 의해 이벤트를 발생시킨 요소의 `부모 요소에도 영향(버블링)`을 미치기 때문에 가능
* 실제로 이벤트를 발생시킨 요소를 알아내기 위해서 Event.target 사용

<br><br>

## 장점

* 많은 핸들러를 할당하지 않아도 되기 때문에 초기화가 단순해지고 `메모리를 절약`
* 요소를 추가하거나 제거할 때 해당 요소에 할당된 핸들러를 추가하거나 제거할 필요가 없기 때문에 `코드가 짧아짐`
* innerHTML이나 유사한 기능을 하는 스크립트로 요소를 더하거나 뺄 수 있기 때문에 `DOM 수정이 쉬움`

<br><br>

## 참고 사이트

> https://poiemaweb.com/js-event  
> https://ko.javascript.info/event-delegation
