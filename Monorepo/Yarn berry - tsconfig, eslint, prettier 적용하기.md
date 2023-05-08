# tsconfig, eslint, prettier 적용하기

## 1. tsconfig 적용하기

워크스페이스 별로 매번 tsconfig를 설정하기가 번거로울수 있습니다.   
이와 같은 문제로 tsconfig base를 생성해서 사용하는 워크스페이스에서 활용하도록 합니다.

### root 폴더에 `tsconfig.base.json` 파일 생성

```json
{
  "compilerOptions": {
    "strict": true,
    "useUnknownInCatchVariables": true,
    "allowJs": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "noEmit": true,
    "esModuleInterop": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "incremental": true,
    "newLine": "lf"
  },
  "exclude": ["**/node_modules", "**/.*/"]
}
```

<br>

### tsconfig 설정이 필요한 다른 워크스페이스에 적용

extends에 `tsconfig.base.json` 을 설정하여, 기본적인 설정을 추가  
💡 워크스페이스마다 필요한 설정이 있을 경우 개별로 작성

#### apps/wanted/tsconfig.json 파일에 extends 추가

```
{
  "$schema": "https://json.schemastore.org/tsconfig",
  "extends": "../../tsconfig.base.json",     // 👈 추가
  "compilerOptions": {
    "baseUrl": "./src",
    "target": "esnext",
    "lib": ["dom", "dom.iterable", "esnext"],
    "module": "esnext",
    "jsx": "preserve",
    "incremental": true,
    "paths": {
      "@/*": ["./*"]
    }
  },
  "exclude": ["**/node_modules", "**/.*/"],
  "include": [
    "next-env.d.ts",
    "**/*.ts",
    "**/*.tsx",
    "**/*.mts",
    "**/*.js",
    "**/*.cjs",
    "**/*.mjs",
    "**/*.jsx",
    "**/*.json"
  ]
}
```

<br>

#### packages/lib/tsconfig.json 파일에 extends 추가

```
{
  "$schema": "https://json.schemastore.org/tsconfig",
  "extends": "../../tsconfig.base.json",     // 👈 추가
  "compilerOptions": {
    "module": "ESNext",
    "moduleResolution": "node",
    "target": "ESNext",
    "lib": ["ESNext", "dom"],
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "baseUrl": "./src",
    "noEmit": false,
    "incremental": true,
    "resolveJsonModule": true
  },
  "exclude": ["**/node_modules", "**/.*/", "./dist", "./coverage"],
  "include": ["**/*.ts", "**/*.js", "**/.cjs", "**/*.mjs", "**/*.json"]
}
```

<br><br>

## 2. eslint, prettier 적용하기

📌 yarn berry는 **순차적으로 설정**하는 것이 중요

### 설치하기

```bash
yarn add prettier eslint eslint-config-prettier eslint-plugin-import eslint-plugin-react eslint-plugin-react-hooks eslint-import-resolver-typescript @typescript-eslint/eslint-plugin @typescript-eslint/parser -D
```

<br>

### 익스텐션/플러그인 설치

`eslint` `prettier` 익스텐션/플러그인 설치

<br>

### prettier 생성

root 폴더에 `.prettierrc` 파일을 생성

```json
{
  "arrowParens": "avoid",
  "bracketSameLine": false,
  "bracketSpacing": true,
  "endOfLine": "lf",
  "jsxSingleQuote": false,
  "printWidth": 120,
  "proseWrap": "preserve",
  "quoteProps": "as-needed",
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5"
}
```

<br>

### prettier 설정 확인

* Webstorm : `settings → prettier 검색 → Automatic Prettier configuration` 지정
* vscode : `.vscode/settings.json` 내용을 추가

```
// .vscode/settings.json

{
  "search.exclude": {
    "**/.yarn": true,
    "**/.pnp.*": true
  },
  "typescript.tsdk": ".yarn/sdks/typescript/lib",
  "typescript.enablePromptUseWorkspaceTsdk": true,
  "eslint.nodePath": ".yarn/sdks",
  "prettier.prettierPath": ".yarn/sdks/prettier/index.js",

  // 기본 포맷터 prettier로 사용
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  // 파일 저장시 formatter 실행
  "editor.formatOnSave": true,
  "editor.rulers": [120]
}
```

<br>

### eslint 생성

root 폴더에 `.eslintrc.js` 파일을 생성

```jsx
module.exports = {
  root: true,

  env: {
    es6: true,
    node: true,
    browser: true,
  },

  parser: '@typescript-eslint/parser',
  parserOptions: {
    ecmaFeatures: { jsx: true },
  },

  extends: [
    'eslint:recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:react/recommended',
    'plugin:react-hooks/recommended',
    'prettier',
  ],
  plugins: ['@typescript-eslint', 'import', 'react', 'react-hooks'],
  settings: {
    'import/resolver': { typescript: {} },
    react: { version: 'detect' },
  },
  rules: {
    'no-implicit-coercion': 'error',
    'no-warning-comments': [
      'warn',
      {
        terms: ['TODO', 'FIXME', 'XXX', 'BUG'],
        location: 'anywhere',
      },
    ],
    curly: ['error', 'all'],
    eqeqeq: ['error', 'always', { null: 'ignore' }],

    // Hoisting을 전략적으로 사용한 경우가 많아서
    '@typescript-eslint/no-use-before-define': 'off',
    // 모델 정의 부분에서 class와 interface를 합치기 위해 사용하는 용법도 잡고 있어서
    '@typescript-eslint/no-empty-interface': 'off',
    // 모델 정의 부분에서 파라미터 프로퍼티를 잘 쓰고 있어서
    '@typescript-eslint/explicit-function-return-type': 'off',
    '@typescript-eslint/no-parameter-properties': 'off',
    '@typescript-eslint/no-var-requires': 'warn',
    '@typescript-eslint/no-non-null-asserted-optional-chain': 'warn',
    '@typescript-eslint/no-inferrable-types': 'warn',
    '@typescript-eslint/no-empty-function': 'off',
    '@typescript-eslint/naming-convention': [
      'error',
      {
        format: ['camelCase', 'UPPER_CASE', 'PascalCase'],
        selector: 'variable',
        leadingUnderscore: 'allow',
      },
      { format: ['camelCase', 'PascalCase'], selector: 'function' },
      { format: ['PascalCase'], selector: 'interface' },
      { format: ['PascalCase'], selector: 'typeAlias' },
    ],
    '@typescript-eslint/explicit-module-boundary-types': 'off',
    '@typescript-eslint/array-type': ['error', { default: 'array-simple' }],
    '@typescript-eslint/no-unused-vars': ['error', { ignoreRestSiblings: true }],
    '@typescript-eslint/member-ordering': [
      'error',
      {
        default: [
          'public-static-field',
          'private-static-field',
          'public-instance-field',
          'private-instance-field',
          'public-constructor',
          'private-constructor',
          'public-instance-method',
          'private-instance-method',
        ],
      },
    ],

    'import/order': [
      'error',
      {
        groups: ['builtin', 'external', 'internal', 'parent', 'sibling', 'index', 'object'],
        alphabetize: { order: 'asc', caseInsensitive: true },
      },
    ],

    'react/prop-types': 'off',
    // React.memo, React.forwardRef에서 사용하는 경우도 막고 있어서
    'react/display-name': 'off',
    'react-hooks/exhaustive-deps': 'error',
    'react/react-in-jsx-scope': 'off',
    'react/no-unknown-property': ['error', { ignore: ['css'] }],
  },
};
```

<br>

### eslint 설정 확인

* Webstorm : `settings → eslint → Automatic Eslint configuration` 지정
* vscode : `.vscode/setting.json` 설정 추가

```
{
  "search.exclude": {
    "**/.yarn": true,
    "**/.pnp.*": true
  },
  "typescript.tsdk": ".yarn/sdks/typescript/lib",
  "typescript.enablePromptUseWorkspaceTsdk": true,
  "eslint.nodePath": ".yarn/sdks",
  "prettier.prettierPath": ".yarn/sdks/prettier/index.js",

  // 기본 포맷터 prettier로 사용
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  // 파일 저장시 formatter 실행
  "editor.formatOnSave": true,
  "editor.rulers": [120],

  // 추가되는 내용
  "eslint.packageManager": "yarn",
  "eslint.validate": ["javascript", "javascriptreact", "typescript", "typescriptreact"]
}
```

<br>

### 워크스페이스별 설정

기존 워크스페이스에 .eslintrc.json 파일과 같은 설정파일이 있다면 삭제  
코드에서 lint 설정이 올바르게 적용 되는지 테스트할 것 

<br>

### Eslint 설정 공유하기

eslint 패키지를 만들어서 공유허는 방법 

[Kakao - ESLint 조금 더 잘 활용하기](https://tech.kakao.com/2019/12/05/make-better-use-of-eslint/)

