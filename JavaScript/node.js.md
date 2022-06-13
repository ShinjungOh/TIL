# Node.js

## 자바스크립트 엔진
React는 JavaScript의 라이브러리 <br>
자바스크립트는 브라우저 내장 자바스크립트 엔진을 이용해 실행된다. <br>
=> `자바스크립트는 웹브라우저에서만 실행될 수 있다?` <br>

<br>

### 자바스크립트 엔진 종류

|  브라우저   |        개발        |      엔진       |
|:-------:|:----------------:|:-------------:|
| Safari  |      Apple       |     Nitro     |
| Firefox |     Mozilla      | Spider Monkey |
| Chrome  |      Google      |    **V8**     |
|  Edge   |    Microsoft     |    Chakra     |
|  Opera  |  Opera Software  |    Presto     |

<br>

## Chrome V8 엔진
* C++로 개발되어 브라우저 내부가 아니어도 어디서나 엔진을 사용 가능
* V8 엔진을 브라우저로부터 독립시켜 JS를 어디서든 사용하도록 만듦 => `Node.js` 

<br>

## Node.js란?
**자바스크립트의 실행환경 (JavaScript Runtime)** <br>
자바스크립트를 브라우저 없이 독립적으로 실행 가능 (한계가 사라짐)
* PC 프로그램 개발 가능
* 웹 서버 개발 가능

<br>

## Web Server
브라우저로부터 웹을 요청받았을 때, 웹을 반환 <br>
* 채팅 서버, 미디어 서버 등
* 서버도 프로그램이기 때문에 만들 수 있다
* URL : 웹 서버의 주소

<br>

## React와의 관계
리액트는 자바스크립트 파일을 쉽게 만들어내는 기술 <br>
리액트로 만든 JS 파일들은 웹브라우저에 전달되었을 때, 프로그램처럼 실행 => `웹 어플리케이션` <br>
node.js를 기반으로 사용

<br>

## 실행방법
> **GUI (Graphic User Interface)** <br>
> 그래픽 아이콘을 기반으로 명령 내리는 방식

> **CLI (Command Line Interface)** <br>
> 터미널에 명령어를 입력해서 명령 내리는 방식

Node.js를 이용해서 JS파일을 실행하려면 운영체제에 명령을 내려야 함 => `CLI 방식이 간편`

<br>

### 실행
> node `파일 이름.js`

<br>

### Common JS 
Node.js가 기본적으로 제공하는 모듈 시스템
* exports, require 등의 내장함수 
* 모듈 시스템 : 모듈을 내보내고, 불러와서 사용하는 기능 제
* 그 외 모듈 시스템 : ES 모듈 
