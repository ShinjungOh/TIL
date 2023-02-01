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
