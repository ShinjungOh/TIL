# new Function

## new Function 문법

`함수 표현식`과 `함수 선언문` 이외에 함수(Function 객체)를 만들 수 있는 방법  
이 방법 외에는 대안이 없을 때 사용

### 단점 

* 보안 문제 및 eval과 유사한(훨씬 덜 심각한) 성능 문제가 발생할 수 있음
  * eval과 달리, Function 생성자는 **전역 범위로 한정된 함수**만 생성

<br><br>

## 사용 방법

```
let func = new Function ([arg1, arg2, ...argN], functionBody);
```

* `arg1, arg2, ... argN` : 형식 인수명으로 사용할 이름
  * 각 이름은 유효한 JavaScript 식별자거나, 쉼표로 구분한 유효한 식별자 목록이어야 함
* `functionBody` : 함수 정의를 구성하는 JavaScript 문을 담은 문자열

<br><br>

## 특징

### 구문 분석 시점

* Function 생성자로 생성한 Function 객체는 **함수를 생성할 때** 구문 분석을 수행     
* 함수 표현식, 함수 선언문으로 함수를 정의한 경우 코드 내에서 **호출한 경우** 나머지 코드와 함께 구문 분석   

=> Function 생성자가 더 비효율적

### new 연산자 

new 연산자를 사용하지 않고 함수로써 Function 생성자를 호출하는 것은 생성자로 호출하는 것과 동일  
new 연산자가 제거됨으로써 코드의 크기를 약간(4 바이트 작게) 줄일 수 있으므로 Function에 대해서는 new 연산자를 사용하지 않는 것이 좋음

<br><br>

## Function의 속성과 메소드

전역 Function 객체는 자신만의 메소드 또는 속성이 없음     
그 자체로 함수이기에 `Function.prototype`에서 **프로토타입 체인**을 통해 일부 메소드 및 속성을 상속받음

<br><br>

## 클로저 

함수는 [[Environment]] 프로퍼티에 저장된 정보를 이용해 자기 자신이 태어난 곳을 기억  
[[Environment]]는 함수가 만들어진 렉시컬 환경을 참조

new Function을 이용해 함수를 만들면 함수의 [[Environment]] 프로퍼티가 현재 렉시컬 환경이 아닌 **전역 렉시컬 환경**을 참조하게 됨  
=> 외부 변수에 접근할 수 없고, **전역 변수에만 접근**할 수 있음 


> 🎯 new Function으로 만든 함수 내부에서 외부 변수에 접근하려 할 때

1. 스크립트가 프로덕션 서버에 반영되기 전, 압축기(minifier) 에 의해 압축될 때 문제가 발생  
   * 압축기는 스크립트에서 주석이나 여분의 공백 등을 없애 코드 크기를 줄여주는 특수한 프로그램 
   * 압축기가 지역 변수 이름을 짧게 바꾸면서 문제가 발생

    > 함수 내부에 let userName라는 변수가 있으면 이 지역변수는 압축기에 의해 let a 등(짧은 이름)으로 대체되는데, 이때 userName 모두가 a로 교체됨     
     userName은 지역변수이고, 함수 외부에선 함수 내부에 있는 변수에 접근할 수 없기 때문에 이렇게 해도 문제가 없음     
     압축기는 단순히 변수를 찾아서 바꾸지 않고 코드 구조를 분석해 기존에 작성한 코드의 기능을 망가뜨리지 않으면서 역할을 수행  

2. 압축기가 동작한 이후엔, new Function으로 만든 함수 내부에서 외부 렉시컬 환경에 접근하려고 할 때 문제가 발생(이미 이름이 변경되었기 때문)

3. new Function으로 만든 함수에 무언갈 넘겨주고 싶다면 **인수**를 사용할 것  
함수로 전달되는 모든 인수는 생성될 함수의 매개 변수 식별자 이름으로 전달되는 순서대로 처리됨

<br><br>

## 참고 사이트 

> https://ko.javascript.info/new-function  
> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function
