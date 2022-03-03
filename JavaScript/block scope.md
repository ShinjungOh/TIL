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

<br>

### this

```js
//함수 스코프
var value = 0
var obj = {
  value: 1,
  setValue: function () {
    this.value = 2;  //this : obj -> obj.value = 2;
    (function () {
      this.value = 3;  //this : window -> window.value = 3; 
                       //전역 value = 3
    })();
  }
}
obj.setValue();
console.log(value);  //3
console.log(obj.value);  //2
```

```js
//블록 스코프
let value = 0
let obj = {
  value : 1,
  setValue : function () {
    this.value = 2
    {
      this.value = 3
    }
  }
}
obj.setValue()
console.log(value)  //0
console.log(obj.value)  //3
```

* 블록 스코프는 this의 영향을 받지 않음 <br>
* 외부의 변수와 별개로 분리된 스코프가 필요할 때,
  내부에서만 쓰고자하는 변수가 있을 때, 블록 스코프로 감싸주면 된다.
* 함수 스코프는 전역객체로 this 바인딩 (블록 스코프는 this 바인딩을 하지 않음)

<br>

### 모든 `문` 형태에 적용


```js
var sum = 0
for (let i = 1 ; i <= 10 ; i++) {
  sum += i
}
console.log(sum)  //55
console.log(i)  //ReferenceError: i is not defined
```
* 블록 스코프 {} 사이에서 선언한 것 외에도, 
for () 안에서 선언한 변수까지도
for문 전체의 블록 스코프에 갇힌다.

```js
{
  let a = 2
  if (a > 1) {
    let b = a * 3
    console.log(b)
  } else {
    let b = a / 3
    console.log(b)
  }
  console.log(b)  //ReferenceError: b is not defined
}
console.log(a)
```

```js
if (Math.random() < 0.5) {
  let j = 0
  console.log(j)
} else {
  let j = 1
  console.log(j)
}
console.log(j)
```

```js
let a = Math.ceil(Math.random() * 3)
switch (a) {
  case 1: {
    let b = 10
    console.log(a + b)
    break
  }
  case 2: {
    let b = 20
    console.log(a + b)  //22
    break
  }
  case 3: {
    let b = 30
    console.log(a + b)
    break
  }
}
console.log(a, b)  //22, ReferenceError: b is not defined
```


