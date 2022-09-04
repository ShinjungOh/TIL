# Data Fetching

## SSR

### Server-side rendering

서버가 데이터를 가져와서 그린다  
함수 getServerSideProps

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

## 참고 사이트

> https://nextjs.org/docs/basic-features/data-fetching/overview
