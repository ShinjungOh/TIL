# Axios

## NODE_ENV 값으로 개발, 배포 환경 세팅하기

프로덕션 및 개발 환경에 따라 다른 구성이 가능함      

Node.js는 항상 개발 환경에서 실행된다고 가정하기 때문에,
`NODE_ENV=production` 환경 변수를 설정하여 프로덕션에서 실행 중임을 Node.js에 알릴 수 있음

<br>

### production

일반적으로 프로덕션 환경 설정은 다음을 보장

* 로깅은 최소한의 필수 수준으로 유지 
* 성능 최적화를 위해 더 많은 캐싱 수준이 발생 
* 조건문을 사용하여 다양한 환경에서 코드를 실행할 수 있음 


<br><br>

## Axios와 사용하기 

### `config.ts` 파일 생성

```ts
export const RUNTIME_ENV = process.env.NODE_ENV === 'development' ? 'development' : 'production';

export const BASE_URL = {
  development: 'http://개발 환경',
  production: 'http://프로덕션 환경',
};
```

<br>

### `http.ts` 파일 생성

axios를 이용하는 `http.ts` 파일 생성   
해당되는 환경에서 `BASE_URL`을 사용할 수 있도록 설정

```ts
import axios, { AxiosRequestConfig } from 'axios';

export const client = axios.create({
    baseURL: BASE_URL[RUNTIME_ENV], // ✅
    timeout: 1000,
});

interface HttpClient extends AxiosRequestConfig {
  get: <T = any>(url: string, config?: AxiosRequestConfig) => Promise<T>;
  post: <T = any>(url: string, data?: any, config?: AxiosRequestConfig) => Promise<T>;
  put: <T = any>(url: string, data?: any, config?: AxiosRequestConfig) => Promise<T>;
  patch: <T = any>(url: string, data?: any, config?: AxiosRequestConfig) => Promise<T>;
  delete: <T = any>(url: string, config?: AxiosRequestConfig) => Promise<T>;
}

export const http: httpClient = client;

// ...
```

<br><br>

## 참고 사이트

> https://nodejs.org/en/learn/getting-started/nodejs-the-difference-between-development-and-production  
> https://axios-http.com/kr/docs/intro  
> https://swagger.io/docs/specification/api-host-and-base-path/
