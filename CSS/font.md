# CSS

## font

* `line-height` : 텍스트의 행간을 설정, 배율, 단위 입력
* `letter-spacing` : 텍스트의 자간을 설정, 양수 음수 단위 입력
* `word-spacing` : 텍스트의 단어 간 간격을 지정 (띄어쓰기로 구분되는 단어)
* `text-align` : 블록요소나 표 안에서 텍스트의 가로 정렬방식을 지정
  * center, left, right, justify(양측 정렬)
* `vertical-align` : 인라인 요소나 표 안에서 텍스트의 세로 정렬 방식을 지정
  * top, middle, bottom
* `text-indent` : 텍스트의 들여쓰기를 설정, 양수, 음수, 퍼센트 지정 
* `text-transform` : 영문 텍스트의 대소문자를 바꿈
  * capitalize(첫 문자들 대문자화), none, uppercase, lowercase
* `word-break` : 텍스트가 콘텐츠박스 영역 밖으로 넘쳤을 때, 어떻게 줄을 바꿀지 설정
  * keep-all(어절 기준), break-all(음절 기준)
* `overflow-wrap` : 단어가 콘텐츠 박스 영역 밖으로 넘쳤을 때, 줄바꿈 여부를 설정
  * normal, break-word(단어를 쪼갬, word-break: keep-all과 비슷) 
* `overflow` : 콘텐츠가 커서 요소 안에서 내용을 다 보여주기 힘들 때 어떤 방식으로 보여줄 지 설정
  * visible, hidden(넘치면 안 보임), scroll, auto(콘텐츠의 크기를 인식해서 스크롤바 여부를 자동으로 결정)
* `text-overflow` : 줄바꿈을 하지 않을 때, 요소 밖으로 넘치는 text를 어떻게 표기 할 것인지 설정
  * clip, ellipsis(말 줄임표 처리)
  * ⚠️ text-overflow를 적용하기 전 선행 조건 1. `white-space : nowrap;` 2. `overflow : hidden;`

<br><br>

## font-family

HTML 요소의 글씨체를 바꿀 때 사용 

```
.선택자 {
	/* 폰트이름에 공백이 있는 경우 */
	font-family: "폰트 이름","폰트 이름2","폰트 이름3"
	
	/* 폰트이름에 공백이 없는 경우 */
	font-family: 폰트이름,폰트이름2,폰트이름3
	
	/* 혼용해서 사용할 경우 */
	font-family: 폰트이름,"폰트 이름2"
}
```

앞에서부터 순서대로 지정한 폰트가 적용

<br><br>


## 웹폰트

해당 폰트 파일이 유저의 컴퓨터에 설치되어 있어야 HTML 문서에 적용이 가능한 단점을 보완하고자 만들어진 것   
**웹폰트**는 사용자가 본인의 컴퓨터에 폰트를 직접 설치하지 않아도 **특정 서버에 위치한 폰트를 다운받아 웹페이지에 표시**

<br>

### 사용 방법

#### 1. 폰트 파일을 직접 다운로드 받아서 적용하는 방법

`@font-face`

1. 웹 폰트 파일을 준비(확장자 명 : woff / woff2 / ttf / eot)
2. css 문서에서 `@font-face`를 이용해 폰트 파일을 불러오기
3. `@font-face` 안에서 해당 폰트 파일을 어떤 이름의 font-family로 지정할 것인지 설정

#### 2. 외부 서비스에서 제공하는 링크를 이용하는 방법 ✅

`@import`, `<link>`

1. google fonts 사이트에 접속 후, 원하는 폰트 옆에 있는 select this style를 클릭
2. use on web 항목에서 import를 선택하고, 해당 `import 구문`을 css파일 내에 입력
3. css rules to specify families를 참고하여 font-family를 적용

> 구글 폰트 https://fonts.google.com/  
> 눈누 https://noonnu.cc/

<br>
<br><br>
