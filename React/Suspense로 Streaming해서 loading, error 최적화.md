# Next.JS

## Suspense로 Streaming해서 loading, error 최적화하기 

## 서스펜스

> 📖 suspense : 중단하다, 멈추다, 유예하다

리액트 17 버전에서 추가된 기능  
로딩용으로 많이 사용 

```tsx
<Suspense fallback={<Loading />}>
  <SomeComponent />
</Suspense>
```

* 페이지에 로딩될 때까지 잠깐 멈추고 로딩을 보여주다가, 로딩이 끝나면 페이지를 보여주는 기능

<br><br>

## error handling 

* 에러 핸들링 -> error boundary
  * 이 페이지에서 에러가 발생했을 때 이 컴포넌트를 띄운다는 뜻
* 둘이 같이 사용할 경우 : `에러 바운더리` > `서스펜스` > `페이지` 계층구조
* 페이지에서 어떤 부분이 로딩되는지가 중요 -> [서스펜스 공식문서](https://react.dev/reference/react/Suspense)에서 확인

* 로딩 중인걸 어떻게 알지? -> 넥스트에서 서버에서 데이터 패치해올 때, 패치하는 것까지 기다림
  * lazy loading 적용되어 있을 때
  * [use](https://react.dev/reference/react/use) 훅으로 값을 가져오는 경우 - 리액트 18 버전에서 새로 나옴
  * 프로미스가 리졸브되기까지 서스펜스가 기다려쥼
  * use는 독특하게 훅이나 컴포넌트 안에서도 if문 또는 try문 안에도 들어갈 수 있음
    * 컴포넌트, 커스텀 훅 내부이긴 해야함. 일반함수 안에서는 X

<br><br>

## 로딩 구현하기 

* 페이지 자체에서는 -> loading.tsx
* 서버 suspense -> fallback에 직접 넣기
* 클라이언트에서의 리액트 쿼리 -> isPending 이용해 보여주기

### loading.tsx

```tsx
import styles from './home.module.css';

export default function Loading() {
    return (
        <div style={{ display: 'flex', justifyContent: 'center' }}>
            <svg className={styles.loader} height="100%" viewBox="0 0 32 32" width={40} >
                <circle cx="16" cy="16" fill="none" r="14" strokeWidth="4"
                        style={{stroke: 'rgb(29, 155, 240)', opacity: 0.2}}></circle>
                <circle cx="16" cy="16" fill="none" r="14" strokeWidth="4"
                        style={{stroke: 'rgb(29, 155, 240)', strokeDasharray: 80, strokeDashoffset: 60}}></circle>
            </svg>
        </div>
    )
}
```

### home.module.css

```css
@keyframes rotating {
  from{
    transform: rotate(0deg);
  }
  to{
    transform: rotate(360deg);
  }
}
.loader {
  animation: rotating 2s linear infinite;
}
```

### 클라이언트 컴포넌트에서 적용하기

```tsx
"use client";

import {InfiniteData, useInfiniteQuery} from "@tanstack/react-query";
import {getPostRecommends} from "@/app/(afterLogin)/home/_lib/getPostRecommends";
import Post from "@/app/(afterLogin)/_component/Post";
import {Post as IPost} from "@/model/Post";
import {Fragment, useEffect} from "react";
import {useInView} from "react-intersection-observer";
import styles from "@/app/(afterLogin)/home/home.module.css";

export default function PostRecommends() {
    const {
        data,
        fetchNextPage,
        hasNextPage,
        isFetching,
        isPending,
        isLoading // isFetching && isPending
    } = useInfiniteQuery<IPost[], Object, InfiniteData<IPost[]>, [_1: string, _2: string], number>({
        queryKey: ['posts', 'recommends'],
        queryFn: getPostRecommends,
        initialPageParam: 0,
        getNextPageParam: (lastPage) => lastPage.at(-1)?.postId,
        staleTime: 60 * 1000, // fresh -> stale time
        gcTime: 300 * 1000,
    });
    const {ref, inView} = useInView({
        threshold: 0,
        delay: 300,
    });

    useEffect(() => {
        if (inView) {
            !isFetching && hasNextPage && fetchNextPage();
        }
    }, [inView, isFetching, hasNextPage, fetchNextPage]);

    if (isPending) { // ✅
        return (
            <div style={{ display: 'flex', justifyContent: 'center' }}>
                <svg className={styles.loader} height="100%" viewBox="0 0 32 32" width={40} >
                    <circle cx="16" cy="16" fill="none" r="14" strokeWidth="4"
                            style={{stroke: 'rgb(29, 155, 240)', opacity: 0.2}}></circle>
                    <circle cx="16" cy="16" fill="none" r="14" strokeWidth="4"
                            style={{stroke: 'rgb(29, 155, 240)', strokeDasharray: 80, strokeDashoffset: 60}}></circle>
                </svg>
            </div>
        )
    }

    return (
        //
    )
}
```

* 처음에는 isPending이 true
  * 데이터를 아예 불러오지 않았을 때
  * 데이터를 가져오는 순간 isFetching이 true가 됨
* 그때 isLoading도 true가 됨 // isFetching && isPending
* isFetching은 데이터를 다시 가져올 때마다(QueryFn이 호출될 때마다) true가 됨
* 초기에 로딩창을 보여줄지 말지는 isPending이나 isLoading 둘 중에 쓰면 됨


* Next에서는 어차피 첫 페이지 데이터는 서버에서 불러서 쓰기 때문에 무의미
* 다른 페이지로 넘어갔다 올 때 로딩창을 띄워주는것
  * 딜레이 적용했는데 로딩창이 바로 안뜨면 캐시 때문이므로 서버를 껐다 켜기
* SSR 안되더라도 검색엔진에 문제 없음. 메타데이터따로 넣어주면 됨

### 서버 suspense 적용하기

```tsx
  <TabProvider>
    <Tab/>
        <PostForm/>
        <Suspense fallback={<Loading/>}>
            <TabDeciderSuspense/>
        </Suspense>
    </TabProvider>
```

<br><br>

## 에러 구현하기 

### 클라이언트 vs 서버

* 클라이언트 컴포넌트에서의 에러는 isError로 처리
  * 직접 isloading, isError 등 받아서 사용
* 서버 컴포넌트에서 에러는 error.tsx, loading.tsx 등을 사용

-> 넥스트에서는 기본적으로 로딩을 서스펜스로 감싸주기 때문에 서스펜스를 직접 쓸 일은 없음

### error.tsx

```tsx
'use client' // Error components must be Client Components

import {useEffect} from 'react'

export default function Error({error, reset,}: {
    error: Error & { digest?: string }
    reset: () => void
}) {
    useEffect(() => {
        // Log the error to an error reporting service
        console.error(error);
    }, [error])

    return (
        <div>
            <h2>Something went wrong!</h2>
            <button
                onClick={
                    // Attempt to recover by trying to re-render the segment
                    () => reset()
                }
            >
                Try again
            </button>
        </div>
    )
}
```

<br><br>

## 서스펜스 장점

A가 프리패치 쿼리 - 딜레이 걸어둔게 여기서 일어남 

![스트리밍_예시.png](..%2FImages%2F%EC%8A%A4%ED%8A%B8%EB%A6%AC%EB%B0%8D_%EC%98%88%EC%8B%9C.png)

Suspense를 사용하면 **특정 부위만 렌더링을 지연**시킬 수 있음 -> 그래서 이름이 Suspense   

서버에서 로딩이 필요한 부분과 로딩이 필요하지 않은 부분을 나눠서,   
로딩이 필요하지 않은 부분만 먼저 화면을 클라이언트로 보내주고  
로딩이 필요한 부분은 로딩 끝난 뒤에 다시 클라이언트로 화면 따로 보내주는 스트리밍 방식   
=> 여러 번 클라이언트로 데이터를 보내줄 수가 있음

나중에 로딩되기를 원하는 부분만 서스펜스로 직접 감싸기  
혹은 로딩이 필요한 부분만 따로 컴포넌트로 빼기

로딩 로직이 반복되는게 싫으면 loading을 중복으로 넣기보다는 useSuspenseQuery로 바꿔서 사용하면 됨    
서스펜스가 인식이 되서 서스펜스의 로딩 상태 부분이 실행됨

useInfiniteQuery는 useSuspenseInfiniteQuery로 교체 가능 

<br><br>

## 참고 사이트

> https://react.dev/reference/react/Suspense  
> https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming  
> https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming#what-is-streaming
> https://nextjs.org/docs/app/building-your-application/routing/error-handling  
> https://react.dev/reference/react/use#displaying-an-error-to-users-with-error-boundary
