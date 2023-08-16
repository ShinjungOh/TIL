# React

## Container 컴포넌트 설계 방식

### 내부의 컴포넌트를 여러 개 만들 때

* 상위 컴포넌트는 Container로 감싸기
* 이름 뒤에 Header, Body, Footer 붙이기

![](../Images/Container_컴포넌트_구분.png)

### 예시

```tsx
<EmotionContainer>
    <h4>감정</h4>
    <EmotionList>
        <>
            {emotionImageSrc.map((el, index) => (
                <EmotionItem key={index} onClick={() => handleClickDiaryEmotion(el.emotion)}>
                    <EmotionHeader>
                        <img src={el.url} alt={el.emotion}/>
                    </EmotionHeader>
                    <EmotionBody>{el.emotion}</EmotionBody>
                </EmotionItem>
            ))}
        </>
    </EmotionList>
</EmotionContainer>
```

```tsx
const EmotionContainer = styled.div`
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 20px 15px 15px 15px;
  margin-top: 20px;
  width: 100%;
  height: auto;
  border-radius: 15px;
  background-color: white;
  border: 1px solid ${styleTokenCss.color.gray5};
  font-size: 14px;

  h4 {
    font-weight: 600;
    color: ${styleTokenCss.color.gray3};
  }
`;

const EmotionList = styled.div`
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 8px;
  margin-top: 13px;
`;

const EmotionItem = styled.div`
  border: 1px solid blue;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
`;

const EmotionHeader = styled.div`
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: 1px solid red;
  width: 55px;
  height: 55px;
  border-radius: 50%;
  background-color: ${styleTokenCss.color.secondary};
  cursor: pointer;
  opacity: 45%;

  img {
    width: 33px;
  }

  :hover {
    opacity: 100%;
  }
`;

const EmotionBody = styled.div`
  border: 1px solid green;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-top: 7px;
  width: 55px;
  font-size: 12px;
  font-weight: 600;
  color: ${styleTokenCss.color.gray3};
`;
```

### 주의점

#### 컴포넌트 구조

스크린샷의 경우에서는 1. 🔵 파란색 컴포넌트 내부에 2. 🔴 빨간색 원과 3. 🟢 초록색 글자 칸을 만들어야 함    
컴포넌트 구조를 원 안에 글자가 들어가도록 구현하고 임의로 `margin, padding` 등으로 간격을 조절하면 안 됨

#### 중복 div

`<h4>감정</h4>` 가 만약 `<div>감정</div>` 였다면, EmotionContainer에서의 CSS 때문에 모든 div가 해당 CSS를 공유하게 되는 문제 발생  
영역의 제목 등이라면 시맨틱하게 h1, h4 등의 태그를 써서 구분하는 것이 좋음

```tsx
const EmotionContainer = styled.div`
  // 생략

  div {
    font-weight: 600;
    color: ${styleTokenCss.color.gray3};
  }
`;
```

