# 배열과 메소드

## 배열 변형 : 배열을 변형시키거나 요소를 재정렬

모든 요소에 함수를 호출하고, **반환된 결과를 가지고 새로운 배열을 만듦**    
배열 요소 전체를 대상으로 함수를 호출하고, 함수 호출 결과를 배열로 반환

<br>

### `map`

```  
arr.map(callback(currentValue[, index[, array]])[, thisArg])
```

<br><br>

## 배열 탐색 : 배열 내에서 무언가를 찾을 때 사용

**조건에 맞는 요소 전체**를 담은 배열을 반환  
함수의 반환 값을 true로 만드는 전체 요소를 반환함

조건을 충족하는 요소가 한 개 -> `arr.find(fn)`  
조건을 충족하는 요소가 여러 개 -> `arr.filter(fn)`

<br>

### `filter`

```  
arr.filter(callback(element[, index[, array]])[, thisArg])
```

<br>

### `find`

객체로 이루어진 배열에서, 특정 조건에 부합하는 객체를 찾는 방법 

```  
arr.find(callback[, thisArg])
```

* 함수가 ture를 반환하면 탐색은 중단되고 **해당 요소의 값**이 반환
* 조건에 해당하는 요소가 없으면 undefined를 반환

<br>

### `findIndex`

find와 동일한 일을 하지만 조건에 맞는 **요소**를 반환하는 대신, **해당 요소의 인덱스**를 반환한다는 점이 다름  

```
findIndex(callbackFn, thisArg)
```

* 배열의 첫 번째 요소에 대한 인덱스를 반환
* 만족하는 요소가 없으면 -1을 반환


<br><br>

## 참고 사이트
> https://ko.javascript.info/array-methods
