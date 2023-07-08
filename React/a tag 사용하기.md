# a tag

## 개념

`href` 특성을 통해 URL로 연결할 수 있는 하이퍼링크를 생성  
`<a>` 안의 콘텐츠는 링크 목적지의 설명을 나타내야 함    
`href`은 `Hypertext REFerence`의 줄임말

<br><br>

## href='#'

href 속성은 앵커 요소가 연결할 URL을 지정  

> href 속성의 값이 '#'인 경우

클릭 시 페이지가 다시 로드되지 않고 현재 페이지에서의 스크롤 위치만 맨 위로 이동  
페이지의 맨 위로 스크롤하는 작업을 수행하기 위해 사용됨 

* 이벤트를 막기 위해 `e.preventDefault()` 사용
* a 태그의 이벤트 타입은 `React.MouseEvent<HTMLAnchorElement>`


<br><br>

## 예시   

```tsx
const handlePageSignup = (e: React.MouseEvent<HTMLAnchorElement>) => {
    e.preventDefault();
    navigate(PATH.SIGN_UP);
};

return (
    <Description>
        회원이 아니신가요?{' '}
        <a href="#" onClick={handlePageSignup}>
            회원가입
        </a>
    </Description>
)
```

<br><br>

## 참고 사이트

> https://developer.mozilla.org/ko/docs/Web/HTML/Element/a
> 
