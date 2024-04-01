# CodeceptJS 

## Custom Helpers

Helper는 다양한 라이브러리 위에 통합 인터페이스를 제공하는 래퍼  

### 반복되는 로그인 로직을 줄이기 위한 방법

1. `Before`, `BeforeEach` 훅 사용 
   * 각 테스트 전에 사전 설정 루틴을 실행할 수 있음
   * -> 로그인 등 반복적인 작업을 중앙 관리
2. 커스텀 헬퍼 또는 커스텀 메소드로 추출 
   * 메소드를 호출해서 사용  

<br>

### 주의점 

* 커스텀 헬퍼의 메소드가 비동기 작업을 수행한다면, **async/await**를 사용해 호출 
  * signIn 메소드 내에서 비동기 작업 (예: 페이지 이동, 요소 클릭 등) 수행 
  * Scenario 블록을 async 함수로 만들기

```js
Feature('My Feature');

Scenario('sign in and check dashboard', async ({ I }) => {
  await I.signIn(); // 커스텀 헬퍼 메소드 호출
  I.see('대시보드'); 
});
```

<br><br>

## Custom Helpers 사용하기

### 1. 헬퍼 생성 

```
npx codeceptjs gh
```

<br>

### 2. `codecept.conf.js` 파일에 헬퍼 등록 

```javascript
/** @type {CodeceptJS.MainConfig} */
exports.config = {
  // ...
  helpers: {
    Playwright: {
      browser: 'chromium',
      url: 'http://localhost:5173',
      show: true,
    },
    CustomHelper: { // ✅
      require: "./helpers/CustomHelper.js"
    },
  },
  // ...
};
```

* 파일 주소에 주의할 것 

<br>

### 3. 헬퍼 구현 

```javascript
const Helper = require('@codeceptjs/helper');

class CustomHelper extends Helper {
  async signIn() {
    const { Playwright } = this.helpers;

    await Playwright.amOnPage('/');

    await Playwright.see('하루한냥');
    await Playwright.see('이메일로 로그인');
    await Playwright.see('카카오로 로그인');

    await Playwright.click('이메일로 로그인');
    await Playwright.see('회원이 아니신가요?');

    await Playwright.fillField('email', '123@gmail.com');
    await Playwright.fillField('password','12345678');
    await Playwright.click('로그인');
  }
}

module.exports = CustomHelper;
```

* CodeceptJS의 커스텀 헬퍼를 정의할 때는 CommonJS 모듈 시스템을 사용해야 함

<br>

### 4. 메소드 호출해서 사용하기 

```js
Feature('Signin Process');

Scenario('render HomePage and signin', async ({ I }) => {
  await I.signIn();
  // ...
});
```

* async/await 사용

<br><br>

## 참고 사이트 

> https://codecept.io/helpers/?#extending-codeceptjs-with-custom-helpers
