# 검색어 하이라이팅

## 구현 방법

1️⃣ 함수를 생성하고, `검색어`와 `해당 검색어에 따른 결과값`을 인자로 받는다.  
2️⃣ 받은 인자끼리 대소문자를 일치시키고 비교하기 위해서 전부 소문자로 변경한다. `toLowerCase()`  
3️⃣ 검색어가 공백이 아니거나, 결과값에 검색어가 포함되어 있을 때, `if (searchValue !== '' && title.includes(searchValue))`  
4️⃣ `new RegExp()`를 활용해 매치되는 검색어를 기준으로 문자열을 배열로 만든다.  

<br><br>

## 정규표현식 플래그

* g = global, 전역 탐색 
* i = case-insensitive, 대소문자를 구분하지 않음

> new RegExp(`(${query})`, 'gi') 의 경우  
queried text가 여러개 존재할 경우 1️⃣모든 queried text를 포함하고, 2️⃣대문자와 소문자 모두 하이라이팅

<br><br>

## 코드 활용

텍스트 하이라이팅 `mark` 태그  
원하는 색상으로 하이라이팅 하려면 `span` 태그  
볼드처리 `strong` 태그

<br>

```tsx
const highlightIncludedText = (text: string, inputValue: string) => {  // 1️⃣ 검색 결과값, 검색어를 인자로 받음
    const title = text.toLowerCase();  // 2️⃣ 검색 결과값
    const searchValue = inputValue.toLowerCase();  // 2️⃣ 검색어(입력어) 
    if (searchValue !== '' && title.includes(searchValue)) {  // 3️⃣ 
        const matchText = text.split(new RegExp(`(${searchValue})`, 'gi'));  // 4️⃣
        console.log(matchText);  // 치아, 암 검색시 각각 ['', '치아', '우식'], ['구강 및 위의 제자리', '암', '종']
        return (
            <>
                {matchText.map((word, index) =>
                    word.toLowerCase() === searchValue ? (  // 입력한 검색어와 문자열 배열의 값을 비교
                        <strong key={index}>
                            {word}  <!-- 일치하는 단어에 볼드처리-->
                        </strong>
                    ) : (
                        word  // 일치하지 않는 단어 아무 처리 x
                    ),
                )}
            </>
        );
    }

    return text;
};
```

```tsx
return (
    <SearchKeywords>
        {
            <>
                {searchedKeywords.map((searchedKeyword, index) => (
                    <li key={searchedKeyword.sickCd}>
                        {
                            highlightIncludedText(searchedKeyword.sickNm, keyword)  // 검색 결과값, 검색어를 인자로 넘김
                        }
                    </li>))
                }
            </>
        }
    </SearchKeywords>
);
```

<br><br>

## 참고 사이트

> https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Regular_Expressions  
> https://developer.mozilla.org/ko/docs/Web/HTML/Element/mark  
> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/split
