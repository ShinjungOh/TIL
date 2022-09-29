# eslint

## ignore

### 파일 내 일부 코드 무시

해당 코드의 바로 윗줄에 추가

```javascript
// eslint-disable-next-line
```

<br>

### 파일 전체 코드 무시

해당 파일의 첫 줄에 추가

```javascript
/* eslint-disable */
```

<br>

### 특정 규칙을 모든 파일에서 무시
`.eslintrc` 파일 “rules”안에 규칙 추가


<br>

### 지정 파일 무시

`package.json` 파일에 추가

```json
“eslintIgnore”: [“file1.js”, “file2.js”]
```

<br>

### 특정 폴더/파일 무시   

`.eslintignore` 파일 생성 후 경로 추가
```
Ex) src/dir/**
```  

<br>
