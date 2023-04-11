# 테스트

## CodeceptJS

인간 친화적인 E2E 테스팅 도구  
단순하면서도 읽기 편함 → 협업과 소통이 편리  
Playwright을 기본으로 쓸 수 있음  

<br> 

### E2E Test

End To End 테스트  
애플리케이션의 흐름을 처음부터 끝까지 테스트하는 것  
실제 사용자 시나리오를 시뮬레이션하고, 통합 및 데이터 무결성을 위해
테스트 중인 시스템과 해당 구성 요소의 유효성을 검사하여 최종 사용자의 경험에서 테스트하는 것

<br><br>

## CodeceptJS vs Playwright

간단한 서비스는 CodeceptJS, 좀 더 복잡하고 자세한 내용을 처리하려면 Playwright을 사용

<br><br>

## 사용 방법

시나리오를 여러개 작성할 수 있음

```js
Feature('My First Test');

Scenario('test something', ({ I }) => {
  I.amOnPage('https://github.com');
  I.see('GitHub');
});
```


```js
Scenario('메뉴판 필터링', ({ I }) => {
  I.amOnPage('/');

  I.see('푸드코트 키오스크');

  I.click({ name: '일식' });
  I.see('기본카레');

  I.click({ name: '중식' });
  I.see('탕수육');

  I.click({ name: '전체' });
  I.see('제육김밥');

  I.fillField('검색', '메가');
  I.see('메가반점');

  I.fillField('검색', '혹등');
  I.see('일식');
});

Scenario('음식 주문하기', ({ I }) => {
  I.amOnPage('/');

  I.click({ name: '#차돌짬뽕' });
  I.click({ name: '#참치김밥' });
  I.click({ name: '#가라아게카레' });
  I.see('27,500원 주문');

  I.click({ name: 'orderReceipt' });
  I.dontSee('영수증 나오는 곳');
  I.see('차돌짬뽕(9,000원)');
  I.see('가라아게카레(14,000원)');
  I.see('총 가격: 27,500원');

  I.wait(8);

  I.see('영수증 나오는 곳');
});
```

<br><br>

## 참고 사이트 

> https://codecept.io/  
> https://katalon.com/resources-center/blog/end-to-end-e2e-testing
