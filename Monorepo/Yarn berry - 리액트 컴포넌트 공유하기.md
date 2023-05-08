# 리액트 컴포넌트 공유하기

## 1. 리액트 컴포넌트 공유하기

### packages/ui 폴더 생성 및 pacakge.json 생성

`packages/ui` 폴더를 생성하고 명령어를 입력

```bash
cd packages/ui
yarn init
```

`package.json` 파일에서 name을 @wanted/ui 로 변경

```bash
{
  "name": "@wanted/ui",
  "packageManager": "yarn@3.5.0"
}
```

* 이름은 임의로 지을 수 있음
* 다른 패키지와 구분하기 위해 @를 붙임 

<br>

### 리액트 dependency 설치

packages/ui 에서 사용할 dependency 설치

💡 워크스페이스를 새롭게 생성한 경우, pnp 에서 이것을 인식해야 함  
생성 후에는 root 폴더에서 **yarn** 명령어를 실행해서 갱신하는 작업이 필요

```bash
# root폴더로 이동
cd ../../

# 갱신
yarn

# install
yarn workspace @wanted/ui add typescript react react-dom @types/node @types/react @types/react-dom -D
```

<br>

### ui 패키지 설정하기

ui 패키지를 tsconfig 설정과 컴포넌트를 하나 만들어서 공유하기 

#### `packages/ui/tsconfig.json`

```json
{
  "$schema": "https://json.schemastore.org/tsconfig",
  "extends": "../../tsconfig.base.json",
  "compilerOptions": {
    "baseUrl": "./src",
    "target": "esnext",
    "lib": ["dom", "dom.iterable", "esnext"],
    "module": "esnext",
    "jsx": "react-jsx",
    "noEmit": false,
    "incremental": true
  },
  "exclude": ["**/node_modules", "**/.*/", "dist", "build"]
}
```

#### `packages/ui/src/index.ts`, `packages/ui/src/Button.tsx` 파일 생성

`packages/ui/src/Button.tsx`

```tsx
import { ButtonHTMLAttributes, MouseEventHandler, ReactNode } from 'react';

export type ButtonProps = ButtonHTMLAttributes<HTMLButtonElement> & {
  children: ReactNode,
  onClick?: MouseEventHandler<HTMLButtonElement>,
};

const Button = (props: ButtonProps) => {
  const { children, onClick, ...other } = props;

  return (
    <button type="button" onClick={onClick} {...other}>
      {children}
    </button>
  );
};

export default Button;
```

`packages/ui/src/index.ts`

```tsx
export { default as Button } from './Button';
```

#### `packages/ui/package.json` main 추가

main을 지정하여 다른 워크스페이스에서 사용할 경우에 참조하도록 설정 

```
{
  "name": "@wanted/ui",
  "packageManager": "yarn@3.5.0",
  "main": "src/index.ts",    // 👈 추가
  "devDependencies": {
    "@types/node": "^18.16.3",
    "@types/react": "^18.2.0",
    "@types/react-dom": "^18.2.1",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "typescript": "^5.0.4"
  }
}
```

<br><br>

## 2. 프로젝트에서 packages/ui 사용하기

### root 폴더에서 pakcages/ui 패키지를 apps/wanted 프로젝트에 설치

```bash
yarn workspace @wanted/web add @wanted/ui
```

<br>

### `apps/wanted/src/pages.tsx` 파일 수정

```tsx
import { sayHello } from '@wanted/lib/src';
import { Button } from '@wanted/ui';
import Image from 'next/image';
import styles from './page.module.css';

export default function Home() {
  return (
    <main className={styles.main}>
      <div>{sayHello()}</div>
      <Button>Click</Button>
```

<br>

### @wanted/web 실행하기

```bash
yarn workspace @wanted/web dev
```

* 이전 버전에선 오류가 발생 

<br>

### `apps/wanted/next.config.js` 설정 추가  

💡 packages/ui 버튼 컴포넌트의 **컴파일** 과정이 필요  
바로 코드로 적용이 되어 브라우저가 타입스크립트를 해석하지 못해서 오류가 발생  
=> `@wanted/web`에서 javascript로 변환(transpile) 필요 

- [Next.js 13.1 부터 `next-transpile-modules` 기능이 내장 되었습니다](https://nextjs.org/blog/next-13-1#built-in-module-transpilation-stable)

Next 버전이 업데이트 되면서 이 기능이 내장되었기 때문에 오류가 발생하지 않을 수 있음

```bash
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  transpilePackages: ['@wanted/ui'],  # 👈 추가
};

module.exports = nextConfig;
```

<br>

### @wanted/web 재실행하기

정상 작동함을 확인 

```bash
yarn workspace @wanted/web dev
```

![](../Images/yarnberry_Button.png)
