# React Router

## 라우팅

네트워크에 있는 트래픽의 경로를 선택하는 프로세스
(어떤 경로를 이용해 데이터를 받아올 것인지 선택)

<br>

## Web에서의 라우팅 
HTTP 리퀘스트(url)를 어떤 특정 페이지로 연결할 것인지 결정하는 메커니즘

<em> 
ex) <br>
www.card-maker.com <br>
www.card-maker.com<strong>/home</strong> <br>
www.card-maker.com<strong>/profile</strong> <br>
www.card-maker.com<strong>/login</strong></em>

<br>

## React
싱글페이지 어플리케이션을 쉽게 만들 수 있는 라이브러리

<br>

## 싱글페이지 어플리케이션
하나의 url로 한 번 페이지가 로딩되면, 그 안에서 사용자가 다른 페이지를 클릭했을 때 새로운 페이지가 열리는 것이 아닌(전체적인 페이지 리프레쉬 x), <br>
부분적인 내용만 업데이트(해당 컴포넌트만 변경)
원하는 데이터를 동적으로 받아와서 동적으로 볼 수 있도록 처리

* 문제점 : 화면 북마크 불가, 뒤로가기/앞으로가기 등의 네비게이션에 포함되지 않음

<br>

## 리액트 라우터
싱글페이지 어플리케이션을 유지하면서, url을 붙일 수 있음(해당 페이지로 이동, 북마크 추가 가능, 네비게이션 추가)