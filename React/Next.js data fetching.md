# Data Fetching

## SSR

### Server-side rendering

서버가 데이터를 가져와서 그린다  
함수 getServerSideProps  
API Routes -> fs는 server side에서만 가능

```javascript
export async function getServerSideProps(context) {
    console.log('server');
    return {
        props: {time: new Date().toISOString()}
    }
}
```

<br><br>

## CSR

### Client-side rendering

클라이언트(브라우저)가 데이터를 가져와서 그린다  
담당 함수는 따로 없고, 기존 react 사용법과 동일  
API Routes 활용

```javascript
const [time, setTime] = useState();

useEffect(() => {
    console.log('client');
    setTime(new Date().toISOString());
}, []);
```

<br><br>

## SSG

### Static-site generation

데이터를 가져와서 정적인 사이트를 그려둔다.     
함수 getStaticProps

* build 필요
* 서버 부하를 줄임
    * SSR의 경우, 많은 사용자가 접속 시 서버에 부하 발생

```javascript
export async function getStaticProps(context) {
    console.log('server');
    return {
        props: {time: new Date().toISOString()}
    }
}
```

<br>

#### getStaticPaths
SSG시 생성할 목록은 getStaticPaths에서 가져옴 (paths 배열 반환)   

getStaticPaths가 반환하는 `fallback` => 빌드시 생성되지 않은 page에 대한 처리

*  false : 처리하지 않음 (404)
* true : loader ✅, 그 후에 화면을 그림 
* blocking : loader ❌, generation 되는 순간 그림

<br><br>

## ISR

### Incremental Static Regeneration

특정 주기로 데이터를 가져와서 정적 사이트에 다시 그려둔다. (SSG + SSR)  
getStaticProps + revalidate

```javascript
export async function getStaticProps() {
    console.log('server');
    return {
        props: {time: new Date().toISOString()},
        revalidate: 1,  // 초 단위
    }
}
```

<br><br>

## pre-render와 SEO

next.js는 기본적으로 모든 페이지를 pre-render  
**pre-render** : 기초적인 UI가 미리 그려져서 내려오는 것 (js 제외)

<br>

**SEO (Search Engine Optimization)**  
CSR만 제공시, 클라이언트(브라우저)처럼 동작하지 않는 검색엔진의 경우, 아무 데이터도 조회할 수 없음  
=> pre-render 해두면 필요한 데이터 제공 가능

<br>

### next.js의 pre-rendering 방식

> **SSG** : 빌드 타임에 pre-render (✅ 권장 - 서버 부하가 적음)  
> **SSR** : 요청 타임에 pre-render

<br>

### SSG의 2가지 상황
1️⃣ Page의 내용이 외부 데이터에 의존적인 상황 -> getStaticProps  
2️⃣ Page Paths까지 외부 데이터에 의존적인 상황 -> getStaticPaths 도 함께 활용해야 함  

`외부 데이터` : 다른 파일 조회, 외부 API 요청, DB 조회 등

<br>

### SSG를 사용하면 좋은 페이지

* 마케팅 페이지
* 블로그 포스트
* E-commerce 상품 목록
* F&Q, 고객센터 
* 사전, 문서

<br>

### SSG 적용 선택 기준

`사용자가 페이지를 요청하기 전에 pre-render할 수 있는가`  <br>

YES ✅ => SSG  
NO ❌ => SSR, CSR, ISR (커스터마이징 된 페이지를 보여줘야 하는 경우 - 로그인 등)

<br><br>

## 참고 사이트

> https://nextjs.org/docs/basic-features/data-fetching/overview  
> https://nextjs.org/learn/basics/data-fetching/blog-data
