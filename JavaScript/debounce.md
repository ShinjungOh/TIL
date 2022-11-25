# debounce

## 개념

연이어 호출되는 함수들 중 마지막 함수(또는 제일 처음)만 호출하도록 하는 것    
동일 이벤트가 반복적으로 시행되는 경우, 마지막 이벤트가 실행되고 나서 일정 시간(밀리 세컨드)동안 해당 이벤트가 다시 실행되지 않으면 해당 이벤트의 콜백 함수를 실행

* 주로 ajax 검색에 자주 사용
  * <em>Ex) `ㄱ, 거, 검, 검ㅅ, 검새, 검색` 과 같이 여러번 api 호출이 일어나는 것을 방지하기 위해 사용</em> 

<br><br>

## 구현

```js
function debounce(callback, limit = 100) {  // 디바운스를 적용할 콜백 함수, 함수가 실행되기 전의 대기 시간 
    let timeout;
    return function (...args) {
        clearTimeout(timeout);  // limit 이내에 함수가 반복 호출될 경우 timeout이 clearTimeout되므로 실행 취소(이전의 요청이 삭제됨) 
        timeout = setTimeout(() => {  // limit 시간 후에 callback.apply 실행
            callback.apply(this, args);  // apply 메소드로 this의 범위 지정  
        }, limit);
    }
}

debounce(callback, 300);
```

* 검색 시 이용자의 타자가 느린 경우는 막을 수 없음
* 결과 반응이 늦게 뜬다는 컴플레인이 있기 때문에, limit에 적절한 시간을 주는 것이 필요

<br><br>

## 참고 사이트
 
> https://www.zerocho.com/category/JavaScript/post/59a8e9cb15ac0000182794fa  
> http://yoonbumtae.com/?p=3584
