# white-space

## 개념

요소가 공백 문자를 처리하는 법을 지정

> 💡 단어 안에서 줄이 바뀌기를 원하는 경우 overflow-wrap, word-break, hyphens 사용

<br><br>

## 구문

```
/* Keyword values */
white-space: normal;
white-space: nowrap;
white-space: pre;
white-space: pre-wrap;
white-space: pre-line;
white-space: break-spaces;

/* Global values */
white-space: inherit;
white-space: initial;
white-space: unset;
```

| 비교  |개행 문자 | 스페이스, 탭 | 자동 줄 바꿈 |줄 끝의 공백 |
|-----|:----:|:-------:|:-------:|:------:|
| normal |  병합  |   병합    |    예    |   제거   |
| nowrap |  병합  |   병합    |   아니오   |   제거   |
| pre |  유지  |   유지    |   아니오   |   유지   |
| pre-wrap |  유지  |   유지    |    예    |   넘침   |
| pre-line |  유지  |   병합    |    예    |   제거   |
| break-spaces |  유지  |   유지    |    예    |  줄 바꿈  |

<br>

### normal

연속 공백을 하나로 합침  
개행 문자도 다른 공백 문자와 동일하게 처리  
한 줄이 너무 길어서 넘칠 경우 자동으로 줄을 바꿈 

### nowrap

연속 공백을 하나로 합침   
줄 바꿈은 `<br>` 요소에서만 일어남

### pre 

연속 공백 유지  
줄 바꿈은 개행 문자와 `<br>` 요소에서만 일어남

### pre-wrap 

연속 공백 유지  
줄 바꿈은 개행 문자와 `<br>` 요소에서 일어나며, 한 줄이 너무 길어서 넘칠 경우 자동으로 줄을 바꿈

### pre-line 

연속 공백을 하나로 합침  
줄바꿈은 개행 문자와 `<br>` 요소에서 일어나며, 한 줄이 너무 길어서 넘칠 경우 자동으로 줄을 바꿈




<br><br>

## 참고 사이트

> https://developer.mozilla.org/ko/docs/Web/CSS/white-space
