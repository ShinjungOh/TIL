# tab focus 이동

## tabIndex 속성  

tabindex 속성이 있는 요소는 포커스가 가능  
속성값은 Tab 키를 눌러 요소 사이를 이동할 때의 순서를 표시해주는 숫자

* `button`, `input`, `select`, `a` : 사용자가 웹 페이지와 상호작용 할 수 있게 도와주는 요소는 focus 지원
* `div`, `span`, `table` : 무언가를 표시하는 용도로 사용하는 요소들은 포커싱 지원하지 않음

<br>

### 주의점

* `tabindex="0"` tabindex 속성이 없는것처럼 동작 
  * 포커스를 이동시킬 때 tabindex=0인 요소는 tabindex가 1보다 크거나 같은 요소보다 나중에 포커스를 받음 
  * 포커스 가능하게 만들지만, 포커스 순서는 기본 순서 그대로 유지하고 싶을 때 사용 
요소의 포커스 우선 순위를 일반 `input`과 같도록 함

* `tabindex="-1"` 스크립트로만 포커스 하고 싶은 요소에 사용
  * Tab키를 사용하면 이 요소는 무시되지만 elem.focus() 메소드를 사용하면 포커싱 됨

<br>

### 스타일

포커스 된 요소는 :focus를 사용해서 스타일을 변경

```css
<style>
  li { cursor: pointer; }
  :focus { outline: 1px dashed green; }
</style>
```

<br><br>

## 활용법

이동하기 원하는 곳에 tabIndex 속성값 부여하기  
map의 경우 `arr.map(function(item, index, array) { });`와 같이 사용하므로 index 값을 tabIndex의 값으로 활용할 수 있다. 


```tsx
<Input type='text' placeholder='🔍 질환명을 입력해 주세요.' onChange={handleChangeInput} value={keyword} tabIndex={1}/>
    {
        isOpenSearchKeywords && (
          <CancelButton onClick={handleCancel} tabIndex={2}>ⅹ</CancelButton>
        )
    }
<Button onClick={handleSubmitKeyword} tabIndex={3}>
  <img src={search_icon} width={20} height={20} alt='search_icon' />
</Button>
 <SearchKeywords>
   {
       <>
         {searchedKeywords.map((searchedKeyword, index) => (
             <li key={searchedKeyword.sickCd}
                 tabIndex={index + 4}
             >
               {highlightIncludedText(searchedKeyword.sickNm, keyword)}
             </li>))
         }
       </>
   }
</SearchKeywords>
```

<br><br>

## 참고 사이트

> https://ko.javascript.info/focus-blur#ref-1736  
