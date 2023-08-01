# range 함수

## range

프로그래밍 언어에서 사용되는 함수(파이썬 등)  
일정한 숫자 범위의 배열을 생성하는 함수  
지정한 시작 값부터 끝 값까지 일정한 간격으로 숫자들의 배열을 생성할 수 있음 

> 💡 자바스크립트에는 range 함수가 내장되어 있지 않음  


### 활용 

* 반복문이나 데이터 생성에 유용하게 사용

<br><br>

## 구현하기

### fill, map 이용하기 

```ts
const range = (length, initial, number = 0) => {
    Array(length).fill(0).map((_, index) => {
        initial + index
    })
}
```

### from 이용하기

```ts
Array.from({ length: count }, (_, index) => start + index * step);
```

<br><br>

## 참고 사이트 

> https://www.freecodecamp.org/news/javascript-range-create-an-array-of-numbers-with-the-from-method/
