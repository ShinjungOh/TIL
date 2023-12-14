# TypeScript

## as const

상수 단언  
값 뒤에 `as const`를 붙이면 타입 지정 가능하며, 읽기전용이 됨  
타입스크립트는 최대한 좁은 타입으로 추론  

⚠️ const 단언문은 let, const 등 변수 선언에 쓰이는 키워드와 별개의 기법

<br><br>

## 비교

### as const ❌

```tsx
const sample = {
    a: 1,
    b: true,
} 
```

![](../Images/as_const1.png)


```tsx
const arr1 = [1, 2, 3];
// number[]
```

<br>

### as const ✅

```tsx
const sample = {
    a: 1,
    b: true,
} as const;
```

![](../Images/as_const2.png)

```tsx
const arr2 = [1, 2, 3] as const;
// readonly [1, 2, 3]
```

* readonly 
* 그 자체로 타입이 지정됨
* 배열을 튜플 타입으로 추론할 때에도 사용 가능 

<br><br>

## 단점

as const를 사용하면 정의한 곳이 아니라 사용한 곳에서 오류가 발생

타입 정의에 실수가 있었을 경우, 오류는 타입 정의가 아니라 호출되는 곳에서 발생
(Ex. 요소가 2개인 퓨틀에 세번째 값을 추가 시)  
-> 여러 겹 중첩된 객체에서 오류가 발생하면 근본적인 원인을 추적하기 어려움

<br><br>

## 참고 사이트 

> <이펙티브 타입스크립트> 아이템 21 - 타입 넓히기  
> <이펙티브 타입스크립트> 아이템 26 - 타입 추론에 문맥이 어떻게 사용되는지 이해하기 
