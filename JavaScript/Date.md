# Date

## Date 개념

날짜를 저장할 수 있고, 날짜와 관련된 메소드도 제공해주는 내장 객체

* 생성 및 수정 시간 저장, 시간 측정 
* 현재 날짜를 출력하는 용도
* 1970년의 첫날을 기준으로 흘러간 밀리초를 나타내는 정수는 `타임스탬프(timestamp)` 라고 부름
  * 1970년 1월 1일 UTC(협정 세계시) 이전 날짜에 해당하는 타임스탬프 값은 음수
* Date 객체의 중심을 구성하는 시간 값은 UTC 기준이지만, 날짜와 시간 등 구성 요소를 가져오는 메소드는 모두 현지(호스트 시스템의 위치)의 시간대를 사용
* 밀리초(1/1000 초) 지원
  * 마이크로초를 지원하지 않음

## 생성자

### `Date`

함수로 호출할 경우 `new Date().toString()`과 동일하게 **현재 날짜와 시간을 나타내는 문자열**을 반환

### `new Date`

생성자로 호출할 경우 **새로운 Date 객체를 반환**

<br><br>

## 정적 메소드

### `Date.now`

1970년 1월 1일 00:00:00 UTC로부터 지난 시간을 **밀리초 단위의 숫자 값**으로 반환   
윤초는 무시

💡 `Date.now`는 `new Date().getTime()`과 동일하지만 중간에 Date 객체를 만들지 않음  
=> new Date().getTime()를 사용하는 것보다 **빠르고 가비지 컬렉터의 일을 덜어준다는 장점**이 있음 

### `Date.parse`

날짜를 나타내는 문자열을 분석한 후, 해당 날짜와 1970년 1월 1일 00:00:00 UTC의 시간 차이를 **밀리초 단위의 숫자 값**으로 반환

* ⚠️ Date.parse를 사용한 날짜 분석은 **브라우저 간 차이 및 일관적이지 못한 동작**을 가지고 있으므로 사용하지 않는 것이 좋음 

### `Date.UTC`

생성자가 받을 수 있는 제일 많은 매개변수(구성요소 각각, 2개~7개)를 동일하게 받아서, 
1970년 1월 1일 00:00:00 UTC의 시간 차이를 **밀리초 단위의 숫자 값**으로 반환  
윤초는 무시

<br><br>

## 인스턴스 메소드 - 날짜 구성요소 얻기

연, 월, 일 등의 값 얻기

### `getFullYear`

연도(네 자릿수)를 반환

> ⚠️ getYear말고 `getFullYear`를 사용할 것  
> 여러 자바스크립트 엔진이 더는 사용되지 않는(deprecated) 비표준 메소드 getYear을 구현하고 있음  
> 이 메소드는 두 자릿수 연도를 반환하는 경우가 있기 때문에 절대 사용해선 안 됨  
> 연도 정보를 얻고 싶다면 getFullYear를 사용할 것 

### `getMonth`

월을 반환(0 이상 11 이하)

### `getDate`

일을 반환(1 이상 31 이하)

### `getHours, getMinutes, getSeconds, getMilliseconds`

시, 분, 초, 밀리초를 반환

### `getDay`

요일을 반환  

일요일을 나타내는 0부터 토요일을 나타내는 6까지의 숫자 중 하나를 반환
getDay에선 항상 0이 일요일을 나타내며, 이를 변경할 방법은 없음  

> ℹ️ 위의 메소드는 모두 현지 시간 기준 날짜 구성요소를 반환

### UTC

메소드 이름에 있는 `get` 다음에 `UTC`를 붙여주면 **표준시(UTC+0) 기준의 날짜 구성 요소**를 반환해주는 메소드 
`getUTCFullYear`, `getUTCMonth`, `getUTCDay`를 만들 수 있음

현지 시간대가 UTC 시간대와 다르다면 실행했을 때 다른 값이 출력

```
// 현재 일시
let date = new Date();

// 현지 시간 기준 시
alert( date.getHours() ); // 3

// 표준시간대(UTC+0, 일광 절약 시간제를 적용하지 않은 런던 시간) 기준 시
alert( date.getUTCHours() ); // 18
```

> ℹ️ 아래 메소드는 표준시(UTC+0) 기준의 날짜 구성 요소를 반환해주는 메소드가 없음

### `getTime`

주어진 일시와 1970년 1월 1일 00시 00분 00초 사이의 간격(밀리초 단위)인 타임스탬프를 반환

### `getTimezoneOffset`

현지 시간과 표준 시간의 차이(분)를 반환

```
// UTC-1 시간대에서 이 예시를 실행하면 60이 출력
// UTC+3 시간대에서 이 예시를 실행하면 -180이 출력
alert( new Date().getTimezoneOffset() ); // 540
```

<br><br>  

## 인스턴스 메소드 - 날짜 구성요소 설정하기

날짜 구성요소 설정하기  

`setFullYear(year, [month], [date])` :  현지 시간 기준으로 연도(네 자리 연도면 네 자리로)를 설정  
`setMonth(month, [date])` : 현지 시간 기준으로 월을 설정  
`setDate(date)` : 현지 시간 기준으로 일을 설정  
`setHours(hour, [min], [sec], [ms])` :  현지 시간 기준으로 시를 설정  
`setMinutes(min, [sec], [ms])` : 현지 시간 기준으로 분을 설정  
`setSeconds(sec, [ms])` : 현지 시간 기준으로 초를 설정  
`setMilliseconds(ms)` : 현지 시간 기준으로 밀리초를 설정  
`setTime(milliseconds)` : 1970년 1월 1일 00:00:00 UTC부터 밀리초 이후를 나타내는 날짜를 설정)  

> `setTime`을 제외한 모든 메소드는 `setUTCHours`같이 표준시에 따라 날짜 구성 요소를 설정해주는 메소드가 존재  
> `setHours`와 같은 메소드는 여러 개의 날짜 구성요소를 동시에 설정할 수 있는데, 인수에 없는 구성요소는 변경되지 않음 

```
let today = new Date();

today.setHours(0);
alert(today); // 날짜는 변경되지 않고 시만 0으로 변경

today.setHours(0, 0, 0, 0);
alert(today); // 날짜는 변경되지 않고 시, 분, 초가 모두 변경(00시 00분 00초).
```

<br><br>

## 인스턴스 메소드 - 문자열로 변환 

날짜와 시간을 특정 형식의 문자열로 변환  
날짜와 시간 정보를 원하는 형식의 문자열로 표현할 때 유용

### `toDateString`

Date의 날짜 부분만 나타내는, 사람이 읽을 수 있는 문자열을 반환

### `toISOString` 
Date를 나타내는 문자열을 ISO 8601 확장 형식에 맞춰 반환

### `toJSON` 

`toISOString`을 사용해서 Date를 나타내는 문자열을 반환   
`JSON.stringify`에서 사용

### `toLocaleDateString` (en-US)

Date의 날짜 부분을 나타내는 문자열을 시스템에 설정된 현재 지역의 형식으로 반환

### `toLocaleFormat`

형식 문자열을 사용해서 Date를 나타내는 문자열을 생성

### `toLocaleString`

Date를 나타내는 문자열을 현재 지역의 형식으로 반환  
`Object.toLocaleString` 메소드를 재정의

### `toLocaleTimeString` (en-US)

Date의 시간 부분을 나타내는 문자열을 시스템에 설정된 현재 지역의 형식으로 반환

### `toString`

`Date를 나타내는 시간 문자열을 반환  
Object.toString` 메소드를 재정의

### `toTimeString` (en-US)

Date의 시간 부분만 나타내는, 사람이 읽을 수 있는 문자열을 반환

### `toUTCString`

Date를 나타내는 문자열을 UTC 기준으로 반환

### `valueOf`

Date 객체의 원시 값을 반환   
Object.valueOf() 메소드를 재정의

<br><br>

## 참고 사이트

> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date  
> https://ko.javascript.info/date  
