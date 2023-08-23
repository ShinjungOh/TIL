# String

## padStart

현재 문자열의 시작을 다른 문자열로 채워, **주어진 길이를 만족하는** 새로운 문자열을 반환     
채워넣기는 대상 문자열의 **시작(좌측)부터 적용됨** 

```
str.padStart(targetLength [, padString]);
```

* `targetLength` : 목표 문자열 길이, 현재 문자열의 길이보다 작다면 채워넣지 않고 그대로 반환
* `padString` : 현재 문자열에 채워넣을 다른 문자열, 문자열이 너무 길어 목표 문자열 길이를 초과한다면 좌측 일부를 잘라서 넣음. 기본값은 " "

### 예시

```js
const str = '200';

str.padStart(5); // "  200"
str.padStart(5, '.'); // "..200"
str.padStart(10, '*'); // "*******200"
```


<br><br>

## padEnd

현재 문자열에 다른 문자열을 채워, **주어진 길이를 만족하는** 새로운 문자열을 반환    
채워넣기는 대상 문자열의 **끝(우측)부터 적용됨**

```
str.padEnd(targetLength [, padString]);
```

* `targetLength` : 목표 문자열 길이, 현재 문자열의 길이보다 작다면 채워넣지 않고 그대로 반환
* `padString` : 현재 문자열에 채워넣을 다른 문자열, 문자열이 너무 길어 목표 문자열 길이를 초과한다면 좌측 일부를 잘라서 넣음. 기본값은 " "


### 예시

```js
const str = '200';

str.padEnd(5); // "200  "
str.padEnd(5, '.'); // "200.."
str.padEnd(5, 'qwerty'); // "200qw"
```

<br><br>

## 참고 사이트 

> padStart : https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/padStart  
> padEnd : https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/padEnd
