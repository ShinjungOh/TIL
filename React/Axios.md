# Axios

## 개념

브라우저와 node.js에서 사용할 수 있는 Promise 기반 HTTP 클라이언트 라이브러리

* 동형(isomorphic application) : 동일한 코드베이스로 브라우저와 node.js에서 실행 가능     
* `서버 사이드`에서는 네이티브 node.js의 http 모듈 사용   
* `클라이언트(브라우저)`에서는 **[XMLHttpRequests](https://developer.mozilla.org/ko/docs/Web/API/XMLHttpRequest)** 사용
  * 서버와 상호작용할 때 사용
  * XHR을 사용하면 새로고침 없이도 URL에서 데이터를 가져올 수 있음
  * 사용자의 작업을 방해하지 않고 페이지의 일부를 업데이트할 수 있음

<br><br>

## 특징

* 브라우저를 위해 XMLHttpRequests 생성
* node.js를 위해 http 요청 생성
* [Promise](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise) API를 지원
  * Promise 객체 : 비동기 작업이 맞이할 미래의 완료 또는 실패와 그 결과 값
* 요청 및 응답 인터셉트
* 요청 및 응답 데이터 변환
* 요청 취소
* JSON 데이터 자동 변환
* [XSRF](https://ko.wikipedia.org/wiki/%EC%82%AC%EC%9D%B4%ED%8A%B8_%EA%B0%84_%EC%9A%94%EC%B2%AD_%EC%9C%84%EC%A1%B0) 를  막기위한 클라이언트 사이드 지원

<br><br>

## 인터셉터 (interceptor)

`then` 또는 `catch`로 처리되기 전에 요청과 응답을 가로채, 원하는 기능을 추가할 수 있음

### 예시

```ts
// 요청 인터셉터 추가하기
axios.interceptors.request.use(function (config) {
    // 요청이 전달되기 전에 작업 수행
    return config;
  }, function (error) {
    // 요청 오류가 있는 작업 수행
    return Promise.reject(error);
  });

// 응답 인터셉터 추가하기
axios.interceptors.response.use(function (response) {
    // 2xx 범위에 있는 상태 코드는 이 함수를 트리거
    // 응답 데이터가 있는 작업 수행
    return response;
  }, function (error) {
    // 2xx 외의 범위에 있는 상태 코드는 이 함수를 트리거
    // 응답 오류가 있는 작업 수행
    return Promise.reject(error);
  });
```

### 활용

```ts
// 요청 인터셉터 
client.interceptors.request.use(handleHeadersWithAccessToken);

// 응답 인터셉터
client.interceptors.response.use(
  (response: AxiosResponse) => response,
  (error: AxiosError) => Promise.reject(error),
);
```

<details>
<summary>AxiosResponse</summary>

```ts
export interface AxiosResponse<T = any, D = any> {
  data: T;
  status: number;
  statusText: string;
  headers: RawAxiosResponseHeaders | AxiosResponseHeaders;
  config: InternalAxiosRequestConfig<D>;
  request?: any;
}
```

</details>

<details>
<summary>AxiosError</summary>

```ts
export class AxiosError<T = unknown, D = any> extends Error {
  constructor(
      message?: string,
      code?: string,
      config?: InternalAxiosRequestConfig<D>,
      request?: any,
      response?: AxiosResponse<T, D>
  );

  config?: InternalAxiosRequestConfig<D>;
  code?: string;
  request?: any;
  response?: AxiosResponse<T, D>;
  isAxiosError: boolean;
  status?: number;
  toJSON: () => object;
  cause?: Error;
  static from<T = unknown, D = any>(
    error: Error | unknown,
    code?: string,
    config?: InternalAxiosRequestConfig<D>,
    request?: any,
    response?: AxiosResponse<T, D>,
    customProps?: object,
): AxiosError<T, D>;
  static readonly ERR_FR_TOO_MANY_REDIRECTS = "ERR_FR_TOO_MANY_REDIRECTS";
  static readonly ERR_BAD_OPTION_VALUE = "ERR_BAD_OPTION_VALUE";
  static readonly ERR_BAD_OPTION = "ERR_BAD_OPTION";
  static readonly ERR_NETWORK = "ERR_NETWORK";
  static readonly ERR_DEPRECATED = "ERR_DEPRECATED";
  static readonly ERR_BAD_RESPONSE = "ERR_BAD_RESPONSE";
  static readonly ERR_BAD_REQUEST = "ERR_BAD_REQUEST";
  static readonly ERR_NOT_SUPPORT = "ERR_NOT_SUPPORT";
  static readonly ERR_INVALID_URL = "ERR_INVALID_URL";
  static readonly ERR_CANCELED = "ERR_CANCELED";
  static readonly ECONNABORTED = "ECONNABORTED";
  static readonly ETIMEDOUT = "ETIMEDOUT";
}
```

</details>



<br><br>

## 참고 사이트 

> [Axios 공식문서](https://axios-http.com/kr/)  
> [axios github](https://github.com/axios/axios)
