# 자바스크립트의 class와 static

## class

클래스는 객체를 생성하기 위한 템플릿(빵 틀)  
자바스크립트는 원래 prototype이라는 것을 기반으로 생성했지만, ES5부터는 class라는 키워드로 클래스를 선언할 수 있음

클래스로부터 객체가 되며, 객체가 컴퓨터상의 메모리에 올라가게 되면 인스턴스가 됨(인스턴스화)    
객체와 인스턴스는 별 차이 없지만, 컴퓨터 메모리에 올라간 것이 인스턴스

### constructor 

개체 초기화를 위한 메소드   
class에는 constructor 한개만 가능

```js
class Rectangle {
    constructor(height, width) {
        this.height = height;
        this.width = width;
    }
}

const p = new Rectangle(); // 값을 널을 수 있다
const p1 = new Rectangle(100, 200); 
const p2 = new Rectangle(500, 500);

console.log(p1, p2);
```

<br><br>

## static

클래스에 대한 정적 메소드 또는 속성을 정의  
클래스의 인스턴스에서 호출이 불가함

1. 중복되는 함수, 데이터를 정의할 때 쓰임(메모리 이점)
2. <i>'이 클래스의 객체들끼리 사용되는 메소드나 속성이다'</i> 라는 명시성의 장점

```js
class Point {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }

    static displayName = "Point";
    static distance(a, b) {
        const dx = a.x - b.x;
        const dy = a.y - b.y;
        return Math.hypot(dx, dy);
    }
}

const a = new Point(1, 1);
const b = new Point(1, 9);
const c = Point.distance(a, b);
console.log(c);
```

<br>

### static 변수를 자주 사용하게 되었을 때 단점

static은 일종의 전역변수라 전역변수의 단점 일부를 가짐   
전역변수와는 다르게 get, set 함수를 만들 수 있음(전역변수보다는 조금 더 간접접근 가능)   
클래스에서 사용된다는 명시성을 가진다는 점 등이 다름

- 동시성 문제 : 여러 스레드에서 해당 전역변수를 참조할 경우 
  - 해당 static 변수가 변경되었을 때 모든 스레드에 영향을 주기 때문에 사이드 이펙트가 일어나 불안전할 수 있음
- 메모리 문제 : 클래스가 생성될 때 메모리를 할당, 프로그램 종료시점에 반환되므로 사용하지 않아도 메모리가 할당되어있음
  - 객체에 집어넣은 메소드의 경우, 사용하지 않을 경우에는 메모리 할당 X
- 테스트 문제 : 단위 테스트 시 해당 메소드, 함수만을 실행해야 하는데, static의 경우 단위적이지 않고 전역적으로 관리되기 때문에 해당 부분을 깨끗하게 테스팅하기 어려움
