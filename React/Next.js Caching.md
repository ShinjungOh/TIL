# Next.js 

## Caching

Next.js에는 여러 종류의 캐시가 존재 

`Request Memoization`, `Data Cache`, `Full Route Cache`, `Router Cache`

4개의 캐시를 도입을 할 가치가 있는지 **캐싱 전략**을 판단해야 함    
캐시 등으로 최적화해서 프론트 서버의 부담을 줄여주는게 좋음

넥스트 13 앱라우터부터는 프론트 서버의 부담이 많이 증가(서버 컴포넌트가 도입되었기 때문)  
-> 캐싱을 적당히 활용하지 않으면 프론트 서버가 터질 수 있음

![caching-overview.png](..%2FImages%2Fcaching-overview.png)

* 넥스트에서는 **빌드 타임**일 때 최대한 최적화를 많이 하면 좋음
* 데이터 소스를 백엔드 서버라고 생각하면 됨 
* Hit : 가져오다 
* Set : 캐시로 저장하다 

<br><br>

## Request Memoization

> 한 페이지를 요청할 때 여러 번 서버에 요청이 가는 중복 요청을 제거

페이지를 처음에 렌더링 할 때 중복된 요청이 있으면 제거해줌   
다음번 페이지 요청이 왔을 때는 캐시들이 전부 초기화되서 다시 새로 가져옴   


### Duration

지속 기간  
한 페이지 렌더링할 때 

### Revalidating

언제 캐시를 무효화하고, 새로 받아올지(캐시 갱신)  
한 페이지 렌더링하면 그 다음엔 새로운 요청을 보냄 

### Opting out

캐시를 사용하지 않을 때

<br><br>

## Data Cache

> 페이지와 상관없이 프론트 서버에서 백엔드 서버, DB로 보낸 요청을 얼마나 오래 캐싱할 것인가    
(얼마동안 프론트 서버가 기억을 할 것인가)

* 데이터 캐시를 캐싱하지 않음 : `{ cache: 'no-store' }),`

### Duration

새로 고침하거나 캐시를 안 쓰지 않는 이상 계속 유지  
한 번 캐싱한 값이 계속 유지 -> ⚠️ Revalidating, Opting out를 잘 해줘야함   
=> 유저가 새로운 데이터를 계속 못 볼 수도 있음 

### Revalidating

* Time-based Revalidation : 일정 시간 지나면 자동으로 캐시 갱신 
* On-demand Revalidation : 직접 코드로 캐시를 갱신 

⚠️ 데이터 캐시는 강력하기 때문에 이거를 잘 조절을 해야함  

> SNS 메인 페이지는 새글을 보기위해 자주 새로고침  
> 블로그, 뉴스 기사 등은 수정도 드물고 오래감 -> 수정할 때 캐시 지우기

* revalidateTag(); : 태그로 캐시 지우기
* revalidatePath(); : 지금 보고 있는 페이지 전체의 캐시 날리기 

### Opting out

라이브러리의 캐싱을 막고 싶을 때 page.js에 다음 코드 추가    

```js
// Opt out of caching for all data requests in the route segment
export const dynamic = 'force-dynamic'
```
 
* 이 페이지에서 보내는 모든 요청을 캐싱하지 않겠다는 의미 

<br><br>

## Full Route Cache

> 페이지를 얼마동안 캐싱할 것인가

Full Route Cache가 제대로 돌아가려면 콘텐츠가 아예 변하지 않아야 함 (SNS와는 잘 맞지 않음)  
매우 정적인 사이트를 만들 것이 아니면 신경쓰지 않아도 됨 

* `no-store`가 하나라도 있으면 Full Route Cache는 의미가 없어짐 
* 데이터 캐시의 영향을 많이 받음 
* cookies, headers, searchParams, useSearchParams 등을 사용하면 Full Route Cache는 동작하지 않음
  * 미리 캐싱해두는 의미가 없어짐

<br><br>

## Router Cache(static vs dynamic)

> 유일하게 클라이언트에서 동작하는 캐시

컴포넌트별로 기억을 해둠  
레이아웃은 재사용하고 페이지는 새로 받아오는 것  
페이지를 새로고침하기 전까지는 계속 유지됨  
라우터 캐시는 끌 수 없음

### static vs dynamic의 기준

* 다이나믹 펑션 사용 X, 데이터 캐시 사용하는 경우만 스태틱
  * 뉴스 기사, 블로그 글 등, 항상 콘텐츠가 고정된 경우 
* 나머지는 전부 다이나믹

* Dynamically Rendered: 30 seconds
* Statically Rendered: 5 minutes

<br><br>

## 참고 사이트

> https://nextjs.org/docs/app/building-your-application/caching
