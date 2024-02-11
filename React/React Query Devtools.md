# React Query 

## Devtools

```
npm i @tanstack/react-query-devtools@5 -D
```

![RQDevtools.png](..%2FImages%2FRQDevtools.png)


### Devtools의 장점

1. 불러온 데이터 정보를 볼 수 있음
   * 데이터 state도 알 수 있음 - fresh, stale, inactive 등
     * state에 따라 데이터를 어떻게 하는지가 다름
   * action이 있음
2. 인터페이스를 표준화
   * 데이터를 가져올 때 항상 존재하는 상태 : `로딩, 성공, 실패` 
   * React Query에서는 다 표준 API로 사용 가능 
   * 로딩, 성공, 실패가 표준화되서 캐싱기능과 합쳐 편리하게 사용
3. 키 시스템 
   * 키에 데이터를 저장 
   * 키를 한번에 갱신할 수도 있음

<br>

### 리덕스 대신 React Query 쓰는 이유

#### Redux 

* 리덕스의 핵심은 데이터를 컴포넌트 간 **공유**하는 것
* 리덕스 사가, 리덕스 툴킷을 써도 서버 데이터 가져와서 state에 넣을 수 있지만, 캐싱이 약함 
* React Query/SWR을 같이 사용하는 이유 (두개는 역할 동일)

#### React Query

* React Query의 핵심은 서버의 데이터를 **가져오는** 것 
* React Query는 캐싱을 잘해줌
* 트래픽이 다 돈이기 때문에, 트래픽 관리를 잘 해야함 
  * -> 최대한 **캐싱**을 많이 해두는게 중요
  * 유저가 빠르게 컨텐츠를 볼 수 있기 때문에 UX 증대

* React Query 자체에서도 컴포넌트 간 데이터 공유가 가능
  * Zustand : 리덕스의 가벼운 버전
  * 컴포넌트 간 공유할 때는 Context API를 써도 됨
* => Zustand, Context API를 주로 쓰고 리덕스는 잘 안씀

#### 캐싱

메모리, DB의 임시 저장소에다 가져온 데이터를 저장 및 재사용할수 있도록 하는 것  

* 일정 기간 마다/특정 행위 마다(Ex. 글 수정 시) 캐시 찾아서 DB와 캐시 같이 업데이트 할 수 있음 

<br><br>

## 데이터 State

> 📌 fresh, fetching, first, stale, inactive 5가지 상태  
> 주로 fresh, stale, inactive 세개만 보게될 것

![RQstate.png](..%2FImages%2FRQstate.png)

* React Query는 모든 값은 fresh가 아니라고 기본값으로 설정 되어있음
* fresh : 기본적으로 서버에서 데이터를 불러오면 fresh 
  * 업데이트 필요 없고 계속 써도 됨
  * 언제까지 fresh인지는 개발자가 정함 -> 직접 설정 필요
* stale : 기회가 되면 항상 데이터를 새로 가져올 것
  * 여기서의 기회는 아래 코드의 옵션 3개가 기준


```tsx
    defaultOptions: {
    queries: {
        refetchOnWindowFocus: false, // 탭전환해서 다시 돌아올 시 
        retryOnMount: true, // 컴포가 다시 마운트될때
        refetchOnReconnect: false, // 인터넷 연결 끊겼다 재접속 시
        retry: false, // 데이터 가져올 때 실패시 몇 번 정도 재시도 할 수 있는 옵션 -> false면 그냥 오류 페이지 
    }
}
```

* fetching : 데이터를 가져올 때, 순간적이라 보기 힘듦
* paused : 잠깐 데이터 가져오는걸 멈추는 기능(인터넷 끊겼을때 등) 
  * 멈춰진 것이 있는지 체크하는 상태
* inactive : 보는 화면에서 React Query로 데이터 받아오는 컴포넌트를 사용하지 않을 경우 inactive
    * 데이터를 사용하는지 유무
    * inactive인 데이터는 전부 5분뒤 사라짐
* 값을 전부 메모리에 저장하는데, 값이 너무 많아지면 메모리가 터질 수 있기 때문에 안 쓰는 데이터를 정리(가비지 컬렉션)
    * 기본 5분으로 설정
* ⚠️ staleTIME은 항상 GC TIME보다 짧아야함
* 일반적으로 GC 타임을 stale 타임보다 더 길게 해야 함


```ts
staleTime: 0
```

* 기본값 0 : 0초뒤 fresh에서 stale로 간다는 뜻
* 컨텐츠의 특성에 따라 staleTime 바꿔주면됨
* 데브툴의 gcTime은 캐시타임 (5버전에서 이름이 변경)
* 가비지 컬렉터 타임은 기본 5분

<br><br>

## Actions

* 액션 이용해 데이터를 새로 가져올 수 있음

![RQactions.png](..%2FImages%2FRQactions.png)

* refetch, invalidate, reset의 차이
* refetch : 누를 때마다 새로 데이터를 가져옴
  * 무조건 새로 가져옴
* invalidate : refetch랑 거의 비슷, 데이터를 새로 가져오고 싶으면 둘 다 해도 됨
  * invalidate은 옵저버가 1이 되는 순간 데이터를 가져옴
  * 옵저버 : 현재 페이지에서 데이터를 사용하고 있는 데이터를 가리킴. 1이면 1개가 사용된다는 뜻
  * 다른 페이지로 이동하면 inactive로 바뀌면서, 옵저버가 0이 됨 
  * invalidate이 refetch보다 효율적
  * inactive일땐 안 가져오고, 현재 화면서 데이터를 쓸때만 다시 가져옴
  * 화면에 안보여도 데이터가 필요할 수 있기 때문에 refetch 써야할 때도 있음
* reset : initialData가 있으면 그 데이터로 리셋되고, 없으면 새로 가져옴
  * 초기데이터로 되돌릴 때 사용
* remove : 제거
* Trigger Loading : 로딩 상태로 만드는 것
* Trigger Error : 에러 상태로 만드는 것

<br><br>

## 참고 사이트

> https://tanstack.com/query/latest/docs/framework/react/overview  
> https://tanstack.com/query/v4/docs/framework/react/devtools
