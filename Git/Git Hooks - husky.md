# Git Hooks - Husky

> https://git-scm.com/book/ko/v2/Git%EB%A7%9E%EC%B6%A4-Git-Hooks  
> https://typicode.github.io/husky/getting-started.html

<br><br>

## husky 설치 방법 1 

### 1️⃣ husky & lint-staged 사용

```
npx mrm lint-staged
```

* mrm : 오픈소스 프로젝트의 환경 설정을 동기화 하기 위한 도구

<br>

### 2️⃣ .husky 폴더 생성

<br>

### 3️⃣ pre-commit 파일 생성 및 husky 설정

**pre-commit** 파일의 설정대로 git commit을 하기전에 npx lint-staged 명령어가 실행

```
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

npx lint-staged
```

<br>

### 4️⃣ `package.json`에서 lint-staged 설정

```json
"lint-staged": {
    "*.{js,jsx,ts,tsx}": "eslint --fix",
    "*.css": "stylelint --fix",
    "*.{js,css,md}": "prettier --write",
    "*.js": "eslint --cache --fix"
  }
```
* 원하는 방식으로 eslint, prettier 설정 가능 
* 커밋 시점에 husky 자동 실행
* eslint 에러 발생 시 커밋 불가

<br><br>

## husky 설치 방법 2

### 1. 설치

```
npm install husky --save-dev
```

<br>

### 2. git hook 활성화

```
npx husky install
```

성공하면 다음과 같은 메시지  

> husky - Git hooks installed

<br>

### 3. `package.json` 스크립트 추가

```
npm pkg set scripts.prepare="husky install"
```

```
// package.json 

{
  "scripts": {
    "prettier:check": "prettier --check \"src/**/*.{ts,tsx}\"",
    "prettier:write": "prettier --write \"src/**/*.{ts,tsx}\"", 
    "prepare": "husky install"
  }
}
```

<br>

### 4. hook에 명령 추가

`""` 안에 허스키가 실행할 명령 추가 

```
npx husky add .husky/pre-commit "npx lint-staged"
```

`.husky` 폴더 안의 pre-commit 파일 

```
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx lint-staged
```

> husky - created .husky/pre-commit

<br>

### 5. `package.json`에서 lint-staged 설정

```
"lint-staged": {
    "*.{ts,tsx}": [
      "npm run lint",
      "npm run prettier:check"
    ]
```

이후 커밋을 시도하면 허스키가 작동 

<br><br>

## 작동 원리

1. 커밋을 시도하면 허스키가 실행됨
2. 허스키 폴더의 `pre-commit` 파일에 추가한 `npx lint-staged` 명령어가 실행됨
3. `package.json`의 lint-staged 설정에 적힌 명령어를 실행
4. script에 적힌 명령어가 실행되며 eslint, prettier 체크 
