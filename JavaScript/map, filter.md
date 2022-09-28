# 배열과 메소드

## `map`

### 배열 변형 : 배열을 변형시키거나 요소를 재정렬

모든 요소에 함수를 호출하고, <u>반환된 결과를 가지고 새로운 배열을 만듦</u>  
배열 요소 전체를 대상으로 함수를 호출하고, 함수 호출 결과를 배열로 반환

<br>

```  
arr.map(callback(currentValue[, index[, array]])[, thisArg])
```

<br><br>

## `filter`

### 배열 탐색 : 배열 내에서 무언가를 찾을 때 사용
<u>조건에 맞는 요소 전체</u>를 담은 배열을 반환  
함수의 반환 값을 true로 만드는 전체 요소를 반환함

조건을 충족하는 요소가 한 개 -> `arr.find(fn)`  
조건을 충족하는 요소가 여러 개 -> `arr.filter(fn)`

<br>

```  
arr.filter(callback(element[, index[, array]])[, thisArg])
```

<br><br>

## 참고 사이트
> https://ko.javascript.info/array-methods
