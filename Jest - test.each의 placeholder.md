# 테스트

## Jest에서 제공하는 placeholder

Jest의 test.each에서 쓰이는 placeholder(자리 표시자)  
테스트 이름에 **변수를 동적**으로 넣을 때 사용  

* %s : 문자열 (string)
* %d or %i : 정수 (integer)
* %f : 부동소수점 수 (floating point number)
* %j : JSON (객체를 JSON 형태로 출력)
* %o : 객체 (object)

<br>

### 예시 

```js
test.each([
  [1000, 1],
  [2000, 2],
])("금액 %i원이 입력되면 로또 %i개를 생성한다", (amount, expectedCount) => {
  const tickets = LottoGenerator.generate(amount);
  expect(tickets.length).toBe(expectedCount);
});
```

* %i → 각각 amount와 expectedCount 변수가 숫자로 들어감
  * "금액 1000원이 입력되면 로또 1개를 생성한다"
  * "금액 2000원이 입력되면 로또 2개를 생성한다"

<br><br>

## 사용 목적

테스트 결과 화면에 더 명확하고 읽기 좋은 설명을 표시하기 위해 사용  
나중에 실패한 테스트를 빠르게 파악할 수 있음  
-> 테스트 결과가 명확해지고 디버깅이 쉬워짐 
