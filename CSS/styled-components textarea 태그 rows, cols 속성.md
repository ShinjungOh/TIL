# styled-components

## textarea 태그 속성값

텍스트 입력 영역 중 보이는 영역의 라인수

* rows - 세로 텍스트 수
* cols - 가로 텍스트 수
  
<br><br>

## 주의사항

* ⚠️ **textarea에 width, height를 줄 경우 rows, cols 속성이 적용되지 않음**
* rows, cols 동시 사용 가능
* 속성에 정의해둔 값을 넘어갈 경우 자동으로 스크롤 생성
* 텍스트 입력 영역의 크기는 width, height 속성을 사용해도 설정 가능

<br><br>

## 속성값 적용 방법

```js
<textarea
    cols="숫자" 
    rows="숫자" 
    name="요소이름" 
    readonly  // or disabled
/>
```

```js
const Textarea = ({
    id,
    name,
    rows,
    placeholder,
    onChange,
    ...props
}: TextAreaProps) => (
    <Container
        id={id}
        name={name}
        rows={5}
        placeholder={placeholder}
        onChange={onChange}
        {...props}
    />
);

const Container = styled.textarea`  // width, height 적용 x
  border: 1px solid #E0E0E0;
  border-radius: 4px;
  padding: 16px 16px 0 16px;
  font-size: 14px;
  outline: none;
  resize: none;
  overflow-y: auto;
`;
```

<br><br>

## 참고 사이트

> https://www.vingle.net/posts/1643222  
> http://www.tcpschool.com/html-tag-attrs/textarea-rows
