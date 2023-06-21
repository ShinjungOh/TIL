# Git Hooks

> https://git-scm.com/book/ko/v2/Git%EB%A7%9E%EC%B6%A4-Git-Hooks

<br>

## husky

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

### 4️⃣ package.json에서 lint-staged 설정

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
