# Next.js

## 넥스트의 배포

1. 스태틱 모드 : 넥스트 서버 없이 완전히 html 페이지만으로 구성된 정적인 사이트
2. 다이나믹 모드 - 기본

<br>
		
### 스태틱 vs 다이나믹 기준 

https://nextjs.org/docs/app/building-your-application/rendering/server-components

|  Dynamic Functions   | Data        | Route                |
|:--------------------:|-------------|----------------------|
|          X           | Cached      | Statically Rendered  |
|          O           | Cached      | Dynamically Rendered |
|          X           | Not Cached  | Dynamically Rendered |
|          O           | Not Cached  | Dynamically Rendered |

<br>

### 스태틱 모드

* [스태틱 모드](https://nextjs.org/docs/pages/building-your-application/deploying/static-exports) 적용하려면 `next.config.js`에서 `output: ‘exports’` 추가
* 빌드하는 순간 모든 컨텐츠가 결정됨
* 넥스트 서버는 필요 없어짐 (서버가 콘텐츠를 그때그때 다르게 불러오는 역할이기 때문)
* 블로그, 뉴스 등은 스태틱 모드로 가능 - 본인 사이트 목적에 따라
* SSG이 스태틱 모드

<br>

### 다이나믹 모드 

* 다이나믹일 땐 ISR 가능
* 풀 라우트 캐시가 ISR과 다를바 없어서 앱라우터에서는 ISR 모드가 별도로 존재하지 않음
  * ISR에는 새로운 컨텐츠가 나오는 것 뿐만 아니라 기존 컨텐츠가 수정되는 것도 있음
  * 기존 컨텐츠가 수정되는 것까지 반영을 하고 싶으면 Invalidation에서 Data Cache Revalidating 한번 해주면 됨

<br><br>

## 빌드

> npm run build - 작성한 코드를 프로덕션용으로 변환, 에러 검사   
> npm start - 실제로 배포된 페이지 

빌드 과정에서 발생하는 오류 해결해주기 

![next_프로젝트_빌드.png](..%2FImages%2Fnext_%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8_%EB%B9%8C%EB%93%9C.png)

* 대부분 다이나믹 
* First Load JS : 각 페이지에 방문했을 때 다운받는 자바스크립트 용량 
  * 너무 많이 받으면 빨간색 
  * 보통 300kb 이하여야 빠르게 로딩 

<br>

### 넥스트의 장점

* 코드 스플리팅 : 페이지별로 코드가 쪼개져 있어서 대부분의 경우 용량이 낮음
  * 용량이 큰 경우 라이브러리 때문인 경우가 많음
  * -> 코드 스플리팅, 트리 쉐이킹 등을 사용

<br><br>

## 배포

넥스트가 기본적으로 서버고 메모리 차지하는 양도 많이 있기 때문에 
무료 서버를 사용할 때 메모리가 부족해서 넥스트 서버 배포가 되지 않음 

-> ⚠️ AWS 등으로 배포해야 하는데 **과금**에 주의

### AWS EC2

https://aws.amazon.com/ko/ec2/?nc2=h_ql_prod_fs_ec2

> 인스턴스 시작 > t2.small > 키 페어 없이 진행 > 보안 그룹 설정 > 인스턴스 시작

* small -> medium 순으로 요금이 비싸짐
* 포트 80으로 교체  
  * 80이 아니면 nginx 등의 별도 설정이 추가로 필요
  * 미들웨어, package.json 등 

```
// package.json
"start": "next start -p 80",
```

> 인스턴스 시작 후 연결 > 노드 설치 > nvm install v버전 > git clone 레포지토리 > 레포지토리로 이동 > npm i   

* 노드 설치 자료 : https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-22-04#option-3-installing-node-using-the-node-version-manager
  * 붙여넣기 단축키가 작동 안 해서 우클릭으로 처리 

> 이미지 최적화 npm i sharp > npm run build

* 이미지 최적화 자료 : https://nextjs.org/docs/app/building-your-application/deploying#image-optimization

<br><br>

## 참고 사이트 

> https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-22-04
