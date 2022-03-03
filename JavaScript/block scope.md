# Block Scope

## 스코프 Scope 
### <strong>함수 스코프</strong> <br>
함수에 의해서 생기는 범위 <br>
변수의 유효범위 = 스코프

<br>

### <strong>블록 스코프</strong> <br>
블록에 의해서 생기는 유효범위 <br>
{중괄호} 에 의해서 변수의 유효범위가 결정됨

<br>

```js
{
  let a = 10
  {
    let a = 20
    console.log(a)
  }
  console.log(a)
}
console.log(a)
```

```js
function hasValue (p) {
  console.log(v)  //undefined
  if (p) {
    var v = 'blue'
    console.log(v)
  } else {
    var v = 'red'
    console.log(v)
  }
  console.log(v)
}
hasValue(10)
```

```js
function hasValue (p) {
  console.log(v)  //v is not defined
  if (p) {
    let v = 'blue'
    console.log(v)
  } else {
    let v = 'red'
    console.log(v)
  }
  console.log(v)
}
hasValue(10)
```

<br><br>

### let, const에 대해서만 동작 
   * var일 경우 블록 스코프의 영향을 받지 않음

<br>

### Hoisting
   * 블록 스코프는 중괄호 {} 에 영향받음
   * 문 자체가 하나의 블록 스코프
     * if문, for문, while문, switch-case문 (문단 : 결과를 리턴하지 않음)
   * 스코프
     * 함수 스코프
     * 블록 스코프
     
```js
if (true) {
  let a = 10
  if (true) {
    console.log(a)  //ReferenceError : a is not defined
    const a = 20
  }
  console.log(a)
}
console.log(a)
```

<br>

호이스팅 될 경우 => a : undefined  
호이스팅 안될 경우 => a : 10

<br>

<strong>기존 var</strong>
1. 변수명만 위로 끌어올리고
2. undefined를 할당한다.

<strong>let, const</strong> 
1. 변수명만 위로 끌어올린다. (변수명과 값이 매칭되지 않은 상태)
   * 호이스팅 되지만, 값을 할당하지 않은 것

<br>

> <strong>TDZ (Temporal Dead Zone) </strong> <br>임시사각지대 
* 정식 명칭은 아니지만 널리 통용됨
* 실제로 변수를 선언한 위치에 오기 전까지는 변수를 호출할 수 없음 = TDZ 
