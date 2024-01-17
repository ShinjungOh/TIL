# MSW

## MSW

* 서버 개발자가 API를 못 만들었어도 요청을 보낼 수 있음 -> 대신 요청에 대한 응답을 MSW로 만들어줘야함
* 백엔드 개발자가 만들어야 할 API를 대신 만드는 셈
  * 대신 DB를 다루진 않고, '어떤 요청을 보내면 이러한 대답을 보내줄 것이다'라고 미리 코딩해놓는 것
  * 가장 좋은 방법은 백엔드 개발자와 미리 의논해서 어떤 형식으로 데이터가 올지 맞춰두면 좋음
  * 이런 경우 타입스크립트가 좋음
    * 데이터의 속성이 달라져도 오류를 알려줘서 실수로 빠트릴 걱정이 없음
    * API로 받아오는 데이터를 안전하게 사용할 수 있음
* 백엔드 개발자가 없을 때도 유용하지만, 개발 환경에서 억지로 에러를 내거나(msw의 응답을 에러로 만들면 됨), 로그인을 안해도 되도록 만들거나(msw로 매번 로그인하게 만들기)할 때도 사용됨

* MSW는 넥스트에서 좀 미완성된 부분이 있어서 매끄럽게 돌아가지 않는 부분이 있음

<br><br>

## MSW 설정하기

```bash
# 설치&초기 세팅
npx msw init public/ --save

# 데브 디펜던시에도 추가  
npm install msw --save-dev 
```

* public에 `mockServiceWorker.js` 파일이 생성되는데, MSW에서 이 파일을 자동으로 브라우저에 설치를 해줌
  * 이 파일의 역할은, 어떤 서버 주소로 요청을 보낼 때 이 서비스 워커가 가로채서, 실제 서버한테 요청을 보내는 것처럼 보이지만 사실은 msw가 가로채서 응답을 주는 것
* 이전에는 개발 환경용 주소, 실제 환경용 주소를 따로 넣어줘서 분기처리를 해줬어야 했음 
  * -> 이제는 항상 실제 주소로만 데이터를 보내도, 개발 서버에서만 msw를 활성화시켜서 실제 서버로 보내는 요청을 가로챔

<br>

### browser.ts, http.ts 파일 생성

* 이 둘의 공통 핸들러도 추가

```tsx
// browser.ts

import {setupWorker} from "msw/browser";
import {handlers} from "./handlers";

// This configures a Service Worker with the given request handlers.
const worker = setupWorker(...handlers);

export default worker;
```

```tsx
// http.ts

import { createMiddleware } from '@mswjs/http-middleware';
import express from 'express';
import cors from 'cors';
import { handlers } from './handlers';

const app = express();
const port = 9090;

app.use(cors({origin: 'http://localhost:3000', optionsSuccessStatus: 200, credential: true}));
app.use(express.json());
app.use(createMiddleware(...handlers));
app.listen(port, () => console.log(`Mock server is running on port: ${port}`));
```

Next.js는 서버/클라이언트에서 둘 다 돌기 때문에 msw를 자연스럽게 돌리는 방식이 아직 나오지 않음  
-> 임시로 노드 서버를 조금 활용함   
=> http.ts  

<br>

### 라이브러리 설치

* msw로 가짜 뫀 서버를 만들때 필요한 라이브러리 설치

```
npm i -D @mswjs/http-middleware express cors  
npm i --save-dev @types/express @types/cors
```

<br>

### handlers.ts

실제로 코딩할것은 다 `handlers.ts`에서 코딩  

* api 별로 어떤 응답을 줄지는 직접 코딩을 해야 함

<br>

### 백엔드 서버 따로 실행하기

`package.json`에 스크립트 추가

```
"mock": "npx tsx watch ./src/mocks/http.ts"
 ```

* 터미널 하나 더 뛰워서 `npm run mock` 명령어 입력 -> MSW 서버가 띄워짐
* 오류나면 포트번호 바꿔서 다시 시도
* 핸들러, http 파일이 바뀌면 알아서 서버가 재시작됨
  * 재시작을 해야 수정한 코드가 반영됨

<br><br>

## .env 파일

환경설정은 모두 `.env` 파일에서 처리 

* 언제 MSW를 적용할지, 적용하지 않을지 판단하려면 -> 컴포넌트 하나를 만들어서 넣어주기
  * `MSWComponent.tsx` - 클라이언트 컴포넌트
  * 전체 `Layout.tsx` Body 안에 import
* 브라우저, 즉 클라이언트 환경에서는 이 파일이 요청을 가로챔 -> http 서버로 보냄

```
NEXT_PUBLIC_API_MOCKING=enabled
```

* enabled 가 아니면 msw가 꺼지는것

<br>

### 개발 환경, 배포 환경

개발 환경용 .env, 배포 환경용 .env가 다름 

* 개발 환경용 : `.env.local`
* 배포 환경용 : `.env`
* 개발 중에는 두 파일 다 실행됨

<br>

### NEXT_PUBLIC_API_MOCKING

* `NEXT_PUBLIC`이 붙으면 브라우저에서 접근 가능 -> 소스폴더에서 이 변수에 접근 가능해짐
  * 브라우저에서 접근 가능한 변수여야할 때는 `NEXT_PUBLIC` 붙임
* `API_MOCKING`만 붙으면 서버에서만 접근 가능(유출 안 됨)
  * 모든 사람이 개발자 도구를 볼수있기 때문에, 개발자 도구를 통해 서버에 중요한 변수나 키가 유출되면 안됨

<br>

### MSW 2 변경사항

```ts
if (typeof window !== 'undefined') {  // MSW 2 버전이 되면서 추가해야 하는 부분
    if (process.env.NEXT_PUBLIC_API_MOCKING === "enabled") {
        require("@/mocks/browser");
    }
}
```

* 윈도우가 존재할 때 = 클라이언트 환경, 브라우저라는 뜻 
* 브라우저에서만 돌아간다는 것을 보장

<br><br>

## 참고 사이트 

> https://mswjs.io/docs/getting-started
