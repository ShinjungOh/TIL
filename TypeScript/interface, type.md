# TypeScript

## interface

인터페이스는 상호 간에 정의한 약속 혹은 규칙  
인터페이스 간 확장 가능

* 객체의 스펙(속성과 속성의 타입)
* 함수의 파라미터 
* 함수의 스펙(파라미터, 반환 타입 등)
* 배열과 객체를 접근하는 방식 
* 클래스

<br>

### 옵션 속성

인터페이스 사용 시, 인터페이스에 정의되어 있는 속성을 모두 필수로 사용하지 않아도 됨    
`?` 붙여 사용

```ts
interface 인터페이스_이름 {
  속성?: 타입;
}
```

<br><br>

## 인터페이스 예시 
```ts
// 인터페이스
interface User {
    age: number;
    name: string;
}

// 변수에 인터페이스 활용
let sj: User = {
    age: 20,
    name: 'sj'
}

// 함수에 인터페이스 활용
function getUser(user: User) {
    console.log(user);
}

const capt = {
    name: 'captain',
    age: 100
}

getUser(capt);

// 함수의 스펙(구조)에 인터페이스 활용
interface SumFunction {
    (a: number, b: number): number;
}

let sum: SumFunction;
sum = function (a: number, b: number): number {
    return a + b;
}

// arrow function
const add = (a: number, b: number): number => {
    return a + b;
}

// 인덱싱
interface StringArray {
    [index: number]: string;
}

let arr: StringArray = ['a', 'b', 'c'];
arr[0] = '10';
// arr[1] = 10;

// 딕셔너리 패턴
interface StringRegexDictionary {
    [key: string]: RegExp;
}

let obj: StringRegexDictionary = {
    // sth: /abc/  정규표현식
    cssFile: /\.css$/,
    jsFile: /\.js$/,
}

Object.keys(obj).forEach(function (value) {
});


// 인터페이스 확장
interface Person {
    name: string;
    age: number;
}

interface Developer extends Person {
    language: string;
}

let student: Developer = {
    name: 'sj',
    age: 20,
    language: 'ts'
}
```


<br><br>

## type 

특정 타입이나 인터페이스를 참조할 수 있는 타입 변수  

타입 별칭은 새로운 타입 값을 하나 생성하는 것이 아니라,
<u>정의한 타입에 대해</u> 나중에 쉽게 참고할 수 있도록 <u>이름을 부여하는 것</u>

```ts
type Person = {
    name: string;
    age: number;
}

let student: Person = {
    name: 'sj',
    age: 20
}

type MyString = string;
let str: MyString = 'hello';

type Todo = { 
    id: string; 
    title: string; 
    done: boolean; 
}
function getTodo(todo: Todo) {
}

// 제네릭
type User<T> = {
    name: T;
}
```

<br><br>

## interface vs type 

인터페이스와 타입 별칭의 가장 큰 차이점 => **💡타입의 확장 가능/불가능 여부**   
* 인터페이스 : 확장이 가능 
* 타입 별칭 : 확장이 불가능

가능한 type 보다 확장 가능한 <u>interface</u>로 선언해서 사용하는 것이 좋음

<br><br>

## 참고 사이트

> https://joshua1988.github.io/ts/guide/interfaces.html  
https://joshua1988.github.io/ts/guide/type-alias.html
