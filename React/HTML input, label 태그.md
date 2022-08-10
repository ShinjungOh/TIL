# HTML

## label 태그

input 태그를 도와주는 역할 <br>
input 태그를 디자인 하기 힘들 때 label 태그로 연결해서 쉽게 디자인하거나 클릭 편의성을 높일 수 있다.

```html
<label for="test">여기를 클릭하세요</label>
<input type="text" id="test">
```

<br><br>

## label for
### 사용법 
`label` 태그에 for 속성을 이용해서, `input` 태그의 id 속성과 연계한다. <br>
=> `label`의 for값과 `input`의 id값을 일치시킨다.

label의 문자 부분을 클릭하면, text 속성값의 입력창에 자동으로 커서가 생성된다.

<br>

### 예시
radio, checkbox 속성값을 사용할 때 (작아서 클릭이 어려운 경우)

<br>

### for 쓰지 않고 label 사용하기
label 태그를 input 태그 바깥에 사용하면, for 속성을 사용하지 않을 수 있다.

```html
<label>
  <input type="checkbox">동의
</label>
```

<br><br>

## React에서 label for 사용하기
>  for 대신에 `htmlFor` 사용

```html
<label htmlFor="test">여기를 클릭하세요</label>
<input type="text" id="test" />
```