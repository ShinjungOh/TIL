# React

## 이미지 디렉토리 관리하기(public, src)

React 애플리케이션에서는 이미지를 public과 src 디렉토리에 넣을 수 있음  
각 디렉토리별 이미지 경로를 설정할 때의 차이가 존재 

<br><br>

## public 

정적 파일을 넣는 디렉토리 (html 파일, img 등)

### public 디렉토리를 사용하는 경우 

* 특정 이름을 가진 파일이 필요할 때 : `manifest.webmanifest` 처럼 build된 결과물에서 특정한 파일 이름이 필요한 경우
* 이미지 파일이 수천 개 있어서 경로를 동적으로 참조해야 할 때
* 번들링된 코드 밖에서 `pace.js` 같은 작은 스크립트를 포함하고 싶을 때
* webpack과 호환되지 않는 라이브러리를 사용해야 할 때 (`<script>` 태그로 라이브러리를 포함해야 할 때)

### 단점 

> public 디렉토리에 넣은 파일은 webpack에 의해 처리되지 않고, 원본이 build 폴더에 복사됨

* 파일이 후처리(post-process) 되거나 경량화(minify)되지 않음
* ⚠️ 파일 경로가 잘못되었거나, 파일이 존재하지 않을 경우 컴파일 단계에서 오류가 발생하지 않고, 사용자가 접근할 때 `404 에러` 발생 
* 결과 파일명에 `content hash`가 포함되지 않기 때문에, 파일이 수정될 때 마다 직접 파일명을 수정하거나 매개변수 쿼리를 추가해야 함

<br><br>

## src 

개발하면서 작업하는 파일을 넣는 디렉토리 (index.js, 리액트 컴포넌트 등 js 파일, css 파일 등)

### 특징 

* 💡 파일을 찾지 못하는 경우, 컴파일 단계에서 에러를 잡을 수 있음 
* `import` 할 경우 참조할 수 있는 경로(path) 문자열을 출력
* 💡 `content hash`가 파일명에 포함되기 때문에, 브라우저가 오래된 버전(파일 수정 전)의 파일을 캐싱하고 있는 경우를 고려하지 않아도 됨  
  * 파일이 변경되었을 때만 hash값이 변경
* 서버 요청 횟수를 줄이기 위해 10,000 bytes 이하의 이미지는 path대신 `data URL`을 반환
  * bmp, gif, jpg, jpeg, png 파일에만 적용
  * SVG 파일 제외
  * 파일 크기 기준(10,000 byte)은 IMAGE_INLINE_SIZE_LIMIT 환경변수로 설정을 변경할 수 있음 

<br><br>

## jsx에서 이미지 경로 설정하기

### 1. public 디렉토리에 있는 이미지 - process.env.PUBLIC_URL

```bash
# 모두 가능 

1. src={`${process.env.PUBLIC_URL}/public_assets/logo512.png`}
2. src={'/public_assets/logo512.png'}
3. src={'public_assets/logo512.png'}
```

```tsx
export function App() {
  return (
    <img
      src={`${process.env.PUBLIC_URL}/public_assets/logo512.png`}
    />
  );
}
```

* `환경변수의 PUBLIC_URL`을 사용하지 않아도 괜찮음
* 파일을 찾지 못할 경우 컴파일 에러는 발생하지 않고 이미지만 깨짐

<br>

### 2. src 디렉토리에 있는 이미지 - import

* `webpack`을 사용하면 CSS 파일을 import 하는 것처럼, 이미지 파일도 import 해서 사용 가능
  * webpack이 이미지 파일을 번들에 포함시킴 
* 파일 최상단에 사용할 모든 이미지를 `import`하는 **동기적**인 방법
* 💡파일을 못찾을 경우 컴파일 에러가 발생 -> 코드를 작성할 때 수정 가능

```bash
# import 이미지 경로 
import logoPath from './src_assets/logo192.png'

# image src 설정
<img src={logoPath} />
```

```tsx
import logo from './src_assets/logo192.png';

export function App() {
  return (
      <img src={logo} />
  );
}
```

<br>

### 3. src 디렉토리에 있는 이미지 - require

* `Node.js` 환경이므로 `require`로 문서 어디서나 파일을 불러올 수 있음
* `inline`으로 src의 이미지 파일경로를 바로 지정할 수 있음
* 처음에 모든 이미지 파일을 import 하지 않아도 됨  

```bash
<img src={require('./src_assets/logo192.png').default} />
```

```tsx
export function App() {
  return (
    <img src={require('./src_assets/logo192.png').default} className='App-logo' alt='React' />
  );
}
```

* default 를 붙이는 이유
  * require를 사용하면 객체 형태로 값이 리턴되기 때문에, default 를 붙이면 문자열 형태 그대로 인식되게 만들어줌

<br><br>

## 참고 사이트 

> https://velog.io/@rimo09/React-Create-react-app-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%97%90%EC%84%9C-%EC%9D%B4%EB%AF%B8%EC%A7%80-%EA%B2%BD%EB%A1%9C%EB%A5%BC-%EC%84%A4%EC%A0%95%ED%95%98%EB%8A%94-4%EA%B0%80%EC%A7%80-%EB%B0%A9%EB%B2%95#-public
