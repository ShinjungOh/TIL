# barrelsby

## 기능 

`barrelsby`는 TypeScript 프로젝트에서 `index.ts` 파일을 생성해주는 라이브러리  
import 문 블록을 단순화하고 관련 기능을 그룹화    
-> 지저분한 import를 깔끔하게 정리하고 모듈화

<br><br>

## 예시

### as is

```tsx
import {DropDown} from "./src/controls/DropDown";
import {TextBox} from "./src/controls/TextBox";
import {CheckBox} from "./src/controls/CheckBox";
import {DateTimePicker} from "./src/controls/DateTimePicker";
import {Slider} from "./src/controls/Slider";
```

### to be

```tsx
import {DropDown, TextBox, CheckBox, DateTimePicker, Slider} from "./src/controls";
// or
import * as Controls from "./src/controls/index";
```

<br><br>

## 사용 방법

### 1. 설치

```
npm install --save-dev barrelsby
```


### 2. `barrels-config.json` 파일 생성

```
{
  "delete": true,
  "directory": [
    "./src/pages",
    "./src/features",
    "./src/shared"
  ],
  "exclude": [
    ".spec.tsx",
    ".test.tsx",
    ".stories.tsx",
    "vite-env"
  ],
  "location": "all",
  "singleQuotes": true
}
```

### 3. `package.json` 파일 수정

```
{
  "scripts": {
    "generate-barrels": "barrelsby --config barrels-config.json"
  },
  "devDependencies": {
    "barrelsby": "^2.0.0"
  }
}
```

### 4. 실행

`generate-barrels` 명령어를 실행하면 `index.ts` 파일이 생성



<br><br>

## 참고 사이트

> https://www.npmjs.com/package/barrelsby
