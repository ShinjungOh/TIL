# prettier, eslint 설치 및 실행 방법

## prettier, eslint를 사용하는 이유

여러 작업자의 코딩 스타일 일치를 위해 린터와 포맷터 사용하는 것이 좋다.  
⚠️개발자는 기계와 툴에 의존해야 한다.

* prettier : 스타일 교정
* eslint : 문법 교정, 버그 회피 


모두 룰 원하는대로 커스터마이징 가능  
💡eslint-config-prettier를 통해 eslint와 prettier의 충돌 방지


<br><br>

## prettier

### 프로젝트 설치

`npm init --yes`  
package.json 생성

<br>

### prettier 추가, 설정

1️⃣ `npm install prettier --save-dev`  
프리티어를 데브 디펜던시에 추가  

2️⃣ .prettierrc.js 파일 생성  

3️⃣ .prettierrc.js에서 필요한 rule 추가

```js
// 예시 rule
// .prettierrc.js

module.exports = {
    printWidth: 100, // printWidth default 80 => 100 으로 변경
    singleQuote: true, // "" => ''
    arrowParens: "avoid", // arrow function parameter가 하나일 경우 괄호 생략
};
```

<br>

### prettier 실행

`npx prettier —write .`  
prettier를 실행


> 실행 명령어 : npx prettier —write .

* --write : 파일을 수정&저장까지 하는 옵션 
* --write 사용 x : 파일을 수정만 하는 옵션

<br><br>

## eslint

### eslint 추가
💡 `npm install eslint-config-prettier --save-dev`  
eslint와 prettier의 충돌 방지를 위해 eslint-config-prettier를 데브 디펜던시에 추가

<br>

### eslint 설정

1️⃣ .eslintrc 파일 생성  
확장자 붙이지 않아도 됨

2️⃣ .eslintrc파일에서 필요한 rule 추가

```js
// 예시 rule
// .eslintrc

{
    "extends": ["react-app", "eslint:recommended"],
    "rules": {
        "no-var": "error", // var 금지
        "no-multiple-empty-lines": "error", // 여러 줄 공백 금지
        "no-console": ["error", { "allow": ["warn", "error", "info"] }], // console.log() 금지
        "eqeqeq": "error", // 일치 연산자 사용 필수
        "dot-notation": "error", // 가능하다면 dot notation 사용
        "no-unused-vars": "error" // 사용하지 않는 변수 금지
    }
}
```

<br>

### extends

extends는 특정 config를 확장해서 사용할 때 이용  
extends 사용 시 eslint-config-prettier를 다 적지 않고, config의 뒷부분만 적어도 됨  

* 개인적으로 룰 추가를 원하면 plugin 이용 
* 이미 만들어진 룰 확장해서 쓰려면 config 이용 (extends로 이용 가능)

```js
"extends": ["prettier"],  // ["eslint-config-prettier"]와 동일한 의미
```

<br>

### eslint 실행

> 실행 명령어 : npx eslint . 

<br>

### eslint의 레벨

린트는 에러, 워닝 두가지 레벨이 존재

<br><br>

## 캐시 파일

모든 파일을 매번 처음부터 다시 검사하기 힘들기 때문에 캐시 파일을 만들어 사용  
추가된 부분만 검사를 진행해 불필요한 리소스 낭비를 줄임  


### eslint
1️⃣ `npx eslint --cache .`  
.eslintcache 파일 생성  

2️⃣ .gitignore 파일에 .eslintcache 파일 추가  

<br>

### prettier
1️⃣ `npx prettier --write --cache .`  
prettier 캐시 파일 생성

💡 프리티어의 캐시 파일은 node_modules 안에 생성되기 때문에, 이미 .gitignore에 node_modules를 추가해 놓았다면 따로 프리티어 캐시 파일을 추가할 필요가 없음

<br>

## 캐시 파일을 간편하게 사용하는 방법

매번 치기 귀찮은 명령어를 package.json 파일의 “scripts”에 추가해둘 수 있음


```json
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",
  "format" : "prettier --write --cache .",
  "lint": "eslint --cache ."
},
```

`npm run format/lint` 등으로 실행
