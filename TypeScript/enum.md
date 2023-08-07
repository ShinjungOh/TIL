# TypeScript

## enum

> `enumeration` : 셈, 계산, 열거, 목록이라는 영어단어의 앞부분만 따서 만든 예약어
 

상수를 정의하는 다양한 방법  
열거형으로 이름이 있는 상수들의 집합을 정의할 수 있음

* 열거형을 사용하면 의도를 문서화 하거나 구분되는 사례 집합을 더 쉽게 만들수 있음 
* TypeScript는 숫자와 문자열 기반 열거형을 제공 
* 열거자 이름들은 일반적으로 해당 언어의 상수 역할을 하는 식별자

<br><br>

## 숫자 열거형 (Numeric enums)

```ts
enum Direction {
  Up = 1,
  Down,
  Left,
  Right,
}
```

* Up이 1 로 초기화된 숫자 열거형을 선언
* 그 지점부터 뒤따르는 멤버들은 **자동으로 증가**된 값을 가짐
* 전부 초기화 하지 않을 수도 있음 (0, 1, 2, 3)

<br><br>

## 문자열 열거형 (String enums)

```ts
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT",
}
```

문자열 열거형은 유사한 개념이지만 런타임에서 열거형의 동작이 약간 다름   
문자열 열거형에서 각 멤버들은 문자열 리터럴 또는 다른 문자열 열거형의 멤버로 상수 초기화 해야함  

<br><br>

## 참고 사이트

> https://ko.wikipedia.org/wiki/%EC%97%B4%EA%B1%B0%ED%98%95  
> https://www.typescriptlang.org/ko/docs/handbook/enums.html
