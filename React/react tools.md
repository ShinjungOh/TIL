# React tools

## node JS 
### 자바스크립트로 프로그래밍이 가능하게 하는 프레임워크

자바스크립트를 실행할 수 있는 환경<br>
운영체제 위에서나, node JS 환경이 있다면 자바스크립트를 실행할 수 있다.<br>
node JS를 이용해 자바스크립트로 스크립트를 만들 수 있다.<br>
백엔드 서버 만들기, 서버사이드 렌더링, 커맨드라인, 스크립트 제작<br>

<br>

## npm
### 패키지 매니저

라이브러리 관리, 패키지 관리를 도움<br>
라이브러리 설치, 버전 업데이트, 삭제 등 (실행은 불가)<br>
`package.json` → 사용 중인 외부 라이브러리, 버전 등의 정보 담김<br>

<br>

## npx
### 패키지 실행 매니저

설치 x, 원하는 라이브러리를 실행할 수 있게 도움

<br>

## yarn 
### 패키지 매니저 (by Facebook)

npm보다 성능 개선됨 : 버전관리, 성능, 보안문제 등<br>
npm 위에서 동작 (호환 가능)<br>

⚠️ eject : 사용 시 다시 되돌릴 수 없음 → 세부설정이 필요한 경우에 사용<br>

<br>

## Babel 
### 자바스크립트 트랜스 컴파일러

ECMA script 2015+ 버전 → 예전 버전으로 변환<br>
최신 버전으로 개발, 배포시 예전 브라우저에서도 작동하는 예전 버전 코드로 변환<br>
타입스크립트, JSX 등, 순수 자바스크립트가 아닌 것 → 자바스크립트로 변환<br>

> 바벨을 통해 변환된 것, 만든 컴포넌트를 HTML과 연결하는 작업 필요 ⇒ `react DOM` <br>
`react DOM` : 제일 상위의 컴포넌트를 연결해줌


<br>

## Webpack 
### 모듈 번들링

소스코드, 리소스 이미지들을 묶어서 번들 단위로 사용자에게 제공하도록 도움<br>
소스코드를 줄여주거나 변수/함수 이름 변경(해커로부터 보호)<br>

<br>

## ESLint
### 코드 체크

코드 오류, 문제 발생시 경고<br>

<br>

## Jest
### 테스팅 프레임워크

유닛 테스트를 도와주는 테스팅 프레임워크<br>

<br>

## PostCSS
### CSS 전처리기
less, sass와 비슷 : 그들이 제공하는 프레임워크에 맞게 css를 작성하면 그 css를 브라우저가 이해할 수 있도록 변환<br>
다양한 플러그인 덕분에 원하는 것을 추가할 수 있다<br>

> **PostCSS** : [https://postcss.org/](https://postcss.org/) <br>
**PostCSS Plugins** : [https://www.postcss.parts/](https://www.postcss.parts/) <br>
**Plugins Github** : [https://github.com/postcss/postcss/blob/master/docs/plugins.md](https://github.com/postcss/postcss/blob/master/docs/plugins.md) <br>

<br>

## Postman 
### API 개발
API 확인, 테스트 가능
> [https://www.postman.com/](https://www.postman.com/)
