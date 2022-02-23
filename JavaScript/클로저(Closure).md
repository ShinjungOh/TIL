## 클로저 (Closure)

### closure
에워싸여져 함께 묶여진 함수 <br>
둘러쌓인 LexicalEnvironment의 참조  

=> <strong>내부함수와 LexicalEnvironment의 조합</strong>

클로저는 함수가 생성될 때 매번 같이 발생

![](../Images/클로저_의미.png)

<br>

### 예제

![](../Images/클로저_예제1.png)

![](../Images/클로저_예제2.png)


<br>

### 정리

![](../Images/클로저_핵심.png)

지역변수가 함수 종료 후에도 사라지지 않게 할 수 있다. <br>
(사용자가 선택적으로 어떤 것은 사라지게, 어떤 것은 사라지지 않게 할 수 있다.)

=> <strong>⭐️함수 종료 후에도 사라지지 않는 지역변수를 만들 수 있다.</strong> <br>
클로저의 가장 큰 이점

<br>

![](../Images/클로저_예제3.png)

![](../Images/클로저_핵심개념1.png)

![](../Images/클로저_핵심개념2.png)