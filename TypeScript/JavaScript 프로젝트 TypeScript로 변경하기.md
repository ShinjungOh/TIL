# JavaScript 프로젝트 TypeScript로 변경하기

## CRA 프로젝트에 TS 적용

1️⃣ 필요한 모듈 추가  
`npm install --save typescript @types/node @types/react @types/react-dom @types/jest`

2️⃣ tsconfig.json 파일 생성  
타입스크립트를 자바스크립트로 변환할 때의 설정을 정의해놓는 파일  
프로젝트를 컴파일하는 데 필요한 루트 파일과 컴파일러 옵션을 지정  
https://www.typescriptlang.org/ko/docs/handbook/tsconfig-json.html


<br><br>

## 오류 해결

> Type 'Element[]' is missing the following properties from type 'ReactElement<any, any>': type, props, key 오류  

프래그먼트 추가하기  
https://ko.reactjs.org/docs/fragments.htm
