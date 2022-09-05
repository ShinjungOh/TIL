# Next.js routing

## Shallow Routing

getServerSideProps, getStaticProps 등을 다시 실행시키지 않고, url을 바꾸는 방법

<br>

💡 **현재 상태를 유지하면서 URL만 바꾸는 경우**  
사용자가 어떤 동작을 하고, 그 기록을 query로 남기고 싶을 때    
data fetching을 일으키고 싶지 않을 때  
(query로 남기면 새로고침을 해도 유지됨)
* Ex) <em>스크롤을 10페이지까지 내린 경우</em> 

<br><br>

## url을 바꾸는 3가지 방식

1️⃣ location.replace("url") -> 로컬 state 유지 ❌ (re-render), date-fetching 발생 ✔️ <br>
2️⃣ router.push(url) -> 로컬 state 유지 ✔️ , date-fetching 발생 ✔️ <br>
3️⃣ router.push(url, as, { shallow: true })️ -> 로컬 state 유지 ✔️, date-fetching 발생 ❌ <br>

* 동일한 페이지에서 query만 바뀌어야 함

<br><br>

## 참고 사이트

> https://nextjs.org/docs/routing/shallow-routing
