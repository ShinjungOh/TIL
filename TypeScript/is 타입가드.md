# TypeScript

## is 타입가드

is 키워드는 **Type Guard(타입 가드)** 방법 중 하나    
as가 특정 변수 하나에 국한된 것이라면, is 키워드는 **한정된 범위 내의 모든 변수에 대해서 일괄적으로 적용**할 수 있는 키워드

<br>

### 타입가드

함수가 호출된 범위 내에서만 **타입을 특정 타입(개발자가 지정한 타입)으로 좁힘**    
is 키워드는 as 키워드와 마찬가지로 **컴파일 단계**에서만 사용됨  
런타임 단계에서는 순수한 js 파일과 동일하게 동작

```tsx
function isString(test: any): test is string{
    return typeof test === "string";
}
```

* 함수를 호출한 범위 내에서 isString의 결과 타입을 string으로 좁힘

<br>

### 주의점

return문의 결과 타입만을 명시해놓을 경우,  
Ex) `function isString(test: any): boolean{ // }`

타입 가드가 제대로 이루어지지 않으며 엄격하게 컴파일 검사를 하지 않음

<br>

### 사용 방법 

```tsx
const answer = [];

// 기본 함수
const isNumber = (value: number | null) => value !== null;

// is 타입가드 함수
const isNumberTypeGuard = (value: number | null): value is number => value !== null;

// filter 안에 들어가는 함수와 동일한 로직
const numbersOnly1 = answer.filter((value: number | null) => value !== null);
const numbersOnly2 = answer.filter(isNumberTypeGuard);
```

<br><br>

## 활용 예시

```tsx
const answer = [];

const handleSubmit = async () => { 
  try {
    const isNumber = (value: number | null): value is number=> value !== null;
    const numbersOnly: number[] = answer.filter(isNumber);
    const responsePostAnswer = await apiPostAnswer('stress', numbersOnly);
  } catch (e) {
    // error 핸들링
  }
}
```
