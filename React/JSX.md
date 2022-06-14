# JSX

## HTML, JSX 차이

자바스크립트와 HTML을 합쳐서 사용할 수 있는 문법

```html
<!--html-->
function App() {
	return <h1 class="title" onclick="">Hello</h1>;
}
```

```jsx
// jsx
function App() {
	const name = 'SJ'
	return <h1 className="title" onClick="">Hello {name}</h1>;
}
```
- 자바스크립트 위에서 간단하게 HTML처럼 기능하도록 만들어짐
- 대문자 이용 (HTML과의 차이점)
- 괄호를 이용해 로직 작성
- 비즈니스 로직 작성 가능

<br><br>

## 문법
### 태그 닫기
* 여는 태그와 닫는 태그가 있어야 함
* 닫는 태그가 없을 경우, self closing tag 사용 : </>

<br>

### 최상위 태그
* 가장 바깥에 위치하는 태그 
* 형제 노드가 있는 경우 묶어줘야 함 : <>또는 <React.Fragment>로 묶어줌

<br>

### 조건부 렌더링
#### 삼항 연산자
> (조건식) ? (참표현식) : (거짓표현식)

<br>

### 중괄호 {} 이용
* 자바스크립트 값을 사용하려면 중괄호 이용 