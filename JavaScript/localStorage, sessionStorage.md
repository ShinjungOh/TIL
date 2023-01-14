# localStorage, sessionStorage

## sessionStorage

웹 스토리지 객체인 Storage에 브라우저 내의 key-value 값을 저장 가능  
페이지를 새로 고침해도, 세션이 바뀌어도 저장한 데이터 유지 

### 특징 

sessionStorage 객체는 localStorage에 비해 자주 사용되진 않음 => 제약이 많이 때문  
⚠️ sessionStorage는 오리진뿐만 아니라 브라우저 탭에도 종속

* sessionStorage는 현재 탭 내에서만 유지 
  * 같은 페이지라도 `다른 탭`에 있으면 다른 곳에 저장
* 하나의 탭에 여러 개의 iframe이 있는 경우엔 동일한 오리진에서 왔다고 취급되기 때문에 sessionStorage가 공유됨 
* 탭을 닫고 새로 열 때는 사라짐 
* 페이지를 새로고침할 때 sessionStorage에 저장된 데이터는 사라지지 않음 

<br><br>

## 세션 스토리지 이용하기

로컬 스토리지 객체와 동일한 메소드, 프로퍼티 제공

> `setItem(key, value)` : key, value 추가   
> `getItem(key)` : 키에 해당하는 value 값 받아오기  
> `removeItem(key)` : 키와 해당 값 삭제  
> `clear()` : 모든 것을 삭제    
> `key(index)` : 인덱스(index)에 해당하는 key 값 받아오기   
> `length` : 전체 item 갯수

<br><br>

## localStorage, sessionStorage 차이점

| --- | localStorage         | sessionStorage                         |
|:---:|----------------------|----------------------------------------|
| 오리진  | 오리진이 같은 탭, 창 전체에서 공유 | 오리진이 같은 브라우저 탭, iframe에서 공유            |
| 저장  | 브라우저를 껐다 켜도 남아있음     | 페이지를 새로고침 해도 남아있지만, 탭이나 브라우저를 종료하면 사라짐 |

<br><br>

## 참고 사이트

> https://ko.javascript.info/localstorage
