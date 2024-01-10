# JavaScript

## Array.at

정숫값을 받아 해당 인덱스에 있는 항목을 반환  
양수와 음수를 사용할 수 있음    

음의 정수는 배열의 마지막 항목부터 거슬러 셈  
마지막(가장 최근) 데이터를 불러오려면 (-1)

<br><br>

## 사용방법

```ts
const array1 = [1, 2, 3, 4, 5];

// index 2 
console.log(array1.at(2)); // 3

// index 4 
console.log(array1.at(4)); // 5

// last index
console.log(array1.at(-1)); // 5
```

<br><br>

## 참고 사이트

> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/at
