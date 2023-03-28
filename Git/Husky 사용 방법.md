# Husky 사용 방법

## Husky를 사용하는 이유

![](../Images/husky.png)

### 자동화의 필요성

eslint, prettier을 도입했더라도 사용자가 사용하지 않으면 효과가 없음  
강제성이 없기 때문  
=> 개인이 매번 확인해서 실행하는 것은 한계가 있기 때문에, 자동화된 툴로 강제 적용이 되도록 하는 것이 필요

> commit된 코드는 무조건 formatting이 완료되어야 하고,   
> push된 코드는 무조건 eslint가 pass된 상태에서 push가 되도록 자동화를 구축해야 함

<br>

### git hook 도입

git hook이란 git에서 특정 이벤트 발생하기 전후로 특정 hook 동작을 실행할 수 있게 하는 것(ex. commit, push)

git hook의 단점은 설정이 까다롭다는 점

* 모든 팀원들이 사전에 repo를 클론받고 메뉴얼하게 사전 과정을 수행해야지만 hook이 실행됨을 보장 
* ⚠️ 실수로라도 사전 과정을 시행하지 않는다면 hook이 실행되지 않음

<br>

### 해결법은 Husky 🐶

husky는 깃 훅 설정을 돕는 npm package  

번거로운 git hook 설정이 편리하다는 장점
* npm install 과정에서 사전에 세팅해둔 git hook을 다 적용시킬 수 있어서, 모든 팀원이 git hook을 실행할 수 있도록 하기 편함 
* husky를 통해서 pre-commit, pre-push hook을 설정할 수 있다. 
* Zero dependencies and lightweight (6 kB) : 안정적이고 가볍다

<br><br>

## Husky를 통한 Git Hook 적용

### 설치 방법

1. `npm install husky --save-dev`

2. (처음 husky 세팅하는 사람만 실행 필요) `npx husky install`

   * `npx husky install` : husky에 등록된 hook을 실제 .git에 적용시키기 위한 스크립트
   * add postinstall script in package.json : 이후에 clone 받아서 사용하는 사람들은 npm install 후에 자동으로 husky install이 될 수 있도록 하는 설정
   
⚠️ git hook이기 때문에, git으로 관리되고 있는 repository여야 함   
안 되어있으면 `git init` 명령어 실행

💡 터미널에 husky - Git hooks installed 라고 뜨면 설치가 잘 된 것

<br>

### 실행 방법

1. scripts 설정

`package.json` 파일에 이전에 추가한 prettier, eslint 설정에 "postinstall": "husky install"을 추가

```json
{
  "scripts": {
      "postinstall": "husky install",
      "format": "prettier --cache --write .",
      "lint": "eslint --cache ."
  }
}
```

<br>

2. add pre-commit, pre-push hook 설정

1️⃣ `npx husky add .husky/pre-commit "npm run format"`
* 허스키에서 add하고, npm run format을 커밋 전에 실행할 것 
* prettier --write --cache . 명령이 실행되고 포맷팅과 파일 저장이 된 후 커밋됨

2️⃣ `npx husky add .husky/pre-push "npm run lint"`
* 푸시 전에 eslint --cache . 명령이 실행 
* 만약 에러 발생 시, 스크립트가 중단 (= 푸시가 되지 않음)

<br>

### 참고사항

eslint의 경우,   
> ⚠️ warning은 경고는 주지만 푸시는 진행  
> 🚨 error는 발생하면 실행중인 script가 종료  

따라서 룰을 error로 설정할 지 warn으로 설정할 지 잘 고려해야함

린트에서 warning도 하나도 허용하지 않도록 엄격하게 제한하려면  
`eslint --max-warings=0` 으로 옵션을 붙여서 스크립트를 실행할 것

<br><br>

## 참고 사이트

> https://git-scm.com/book/ko/v2/Git%EB%A7%9E%EC%B6%A4-Git-Hooks  
> https://typicode.github.io/husky/#/?id=articles
