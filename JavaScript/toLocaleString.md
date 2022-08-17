# toLocaleString

## 사용법
```
toLocaleString()
toLocaleString(locales)
toLocaleString(locales, options)
```

<br><br>

## 매개변수

### `locales`
대상을 지정할 때 사용할 언어 환경을 선택  
기본값은 브라우저의 현재 언어 환경

<br>

### `options`

출력 형식 결정  
weekday, year, month, day, hour, minute, second가 모두 undefined 이면, "numeric"

<br><br>

## `options` 매개 변수의 선택값

* localeMatcher
* timeZoneName
* hour12
* hourCycle
* formatMatcher
* weekday
* era
* year
* month
* day
* hour
* minute
* second

<br>

### ⏰ hour12 
12시간제, 24시간제 표기

* boolean 형식
* 기본값 true

```javascript
let date = new Date();
console.log(date.toLocaleString('zh', {hour12: true}));  // 2019/5/12   2:53:49
console.log(date.toLocaleString('zh', {hour12: false})); // 2019/5/12  14:53:49 
```

<br>

### 🗓 year, day, hour, minute, second
numeric, 2-digit : 두 개의 숫자로 표시할 수 있는지

```javascript
let date = new Date();
console.log(date.toLocaleString('zh', {year: 'numeric', month: 'numeric',  day: 'numeric',  hour: 'numeric',  minute: 'numeric',  second: 'numeric'}));  // 2019/5/12  3:05:27
console.log(date.toLocaleString('zh', {year: '2-digit',  month: '2-digit',  day: '2-digit',  hour: '2-digit',  minute: '2-digit',  second: '2-digit'})); // 19/05/12   3:05:27
```

<br>

### 📅 weekday, month
narrow, short, long 

* narrow: 줄일 수 있는 만큼 줄임 
* short: 줄임말 형식
* long: 정상 형식

```javascript
let date = new Date();
console.log(date.toLocaleString('en', { month: 'narrow' }));   // M
console.log(date.toLocaleString('en', {  month: 'short' }));   // May
console.log(date.toLocaleString('en', {  month: 'long' }));    // May

console.log(date.toLocaleString('en', {  weekday: 'narrow'})); // S
console.log(date.toLocaleString('en', { weekday: 'short'}));   // Sun
console.log(date.toLocaleString('en', {  weekday: 'long'}));   // Sunday
```

<br><br>

## 참고 사이트

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString
> https://intrepidgeeks.com/tutorial/tolokalin
