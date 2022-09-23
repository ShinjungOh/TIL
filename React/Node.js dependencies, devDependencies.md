# npm

`package.json`의 dependencies와 devDependencies

<br><br>

## dependencies

`npm install --save`  
`yarn add [package]`  

개발을 할 때 실질적으로 필요한 패키지    
* 패키지를 활용할 때 필요한 디펜던시 
* 기술 스펙으로 모듈 자체가 필요한 라이브러리(런타임) 추가

<br><br>

## devDependencies

`npm install --save-dev`  
`yarn add -D [package]`  

개발, 테스트에 필요한 라이브러리(컴파일-빌드 시 필요) 추가  
* 배포될 때 필요 없는 디펜던시이므로, 빌드 시 해당 디펜던시는 설치되지 않음 
* 빌드할 때 필요한 babel, webpack, file-loader 등 컴파일 할 때 필요한 의존성 추가
 

<br><br>

## 차이

* dependencies와 devDependencies의 차이는 배포용 패키지(실제 상품에서 사용할 패키지)와 개발용 패키지(테스트 패키지 등)의 차이
* 프로젝트를 개발/테스트하려는 것이 아니라, 활용만 하려는 목적이라면 개발의존성을 설치가 불필요 -> devDependencies 제외하고 설치 가능


