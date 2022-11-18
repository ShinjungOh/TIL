# getElementById, querySelector

## getElementById, querySelector 공통점

요소들이 가까이 붙어있지 않은 경우,  
상대 위치를 이용하지 않으면서 웹 페이지 내에서 원하는 요소 노드에 접근하는 방법

* 더 구체적인 엘리먼트를 선택하고 싶다면 querySelector, querySelectorAll 
* getElementByID가 더 빠르고 잘 지원됨

<br><br>

## getElementById

요소에 id 속성이 있을 때

`document.getElementById`

id가 있으면 위치에 상관없이 메소드 `document.getElementById(id)`를 이용해 접근    
getElementById는 `document` 객체를 대상으로 해당 id를 가진 요소 노드를 찾아줌  
document에 구체적인 id의 엘리먼트가 없으면 null 반환

⚠️ 문서 내 요소의 id 속성값은 중복 불가  
⚠️ 문서 노드가 아닌 다른 노드엔 호출 불가

<br><br>

## querySelector

`querySelector`

elem.querySelector(selectors)는 주어진 CSS 선택자에 대응하는 요소 중 첫 번째 요소를 반환  
일치하는 엘리먼트가 없으면 null 반환

* `elem.querySelectorAll`은 선택자에 해당하는 모든 요소를 검색해 첫 번째 요소만을 반환
* `elem.querySelector`는 해당하는 요소를 찾으면 검색을 멈춤 -> `querySelector`가 더 빠른 이유 

<br><br>

## 참고 사이트

> https://ko.javascript.info/searching-elements-dom  
> https://velog.io/@chloeee/getElementById-%EA%B7%B8%EB%A6%AC%EA%B3%A0-querySelector-%EC%B0%A8%EC%9D%B4%EC%A0%90
