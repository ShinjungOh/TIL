## HTTP API 설계 예시

### 3가지 예시

* <strong>HTTP API - 컬렉션</strong>
  * <strong>POST 기반 등록</strong> 
  * <em>Ex) 회원 관리 API 제공</em>
  * <strong>서버가 리소스 URI 결정</strong>


* <strong>HTTP API - 스토어</strong> 
  * <strong>PUT 기반 등록</strong> 
  * <em>Ex) 정적 컨텐츠 관리, 원격 파일 관리</em> 
  * <strong>클라이언트가 리소스 URI 결정</strong>


* <strong>HTML FORM 사용</strong> 
  * 웹 페이지 회원 관리 
  * GET, POST만 지원
  * 순수 HTML + HTML form 사용
  
<br>

### 회원 관리 시스템 
<strong>API 설계 - POST 기반 등록</strong>
* <strong>회원</strong> 목록 /members -> <strong>GET</strong> 
* <strong>회원</strong> 등록 /members -> <strong>POST</strong>
* <strong>회원</strong> 조회 /members/{id} -> <strong>GET</strong> 
* <strong>회원</strong> 수정 /members/{id} -> <strong>PATCH, PUT, POST</strong> 
* <strong>회원</strong> 삭제 /members/{id} -> <strong>DELETE</strong>

<em>/members 같은 것을 '컬렉션'이라고 한다.</em>

<br>

<strong>⭐️POST - 신규 자원 등록 특징</strong>
* 클라이언트는 등록될 리소스의 URI를 모른다. 
* 회원 등록 /members -> POST 
* POST /members


* 서버가 새로 등록된 리소스 URI를 생성해준다. 
  * HTTP/1.1 201 Created <br>
  Location: <strong>/members/100</strong>


* 컬렉션(Collection)
  * 서버가 관리하는 리소스 디렉토리 
  * 서버가 리소스의 URI를 생성하고 관리 
  * 여기서 컬렉션은 /members


* 실무에서는 대부분 POST 기반 컬렉션 사용

<br>

### 파일 관리 시스템 
<strong>API 설계 - PUT 기반 등록</strong>
* <strong>파일</strong> 목록 /files -> <strong>GET</strong> 
* <strong>파일</strong> 조회 /files/{filename} -> <strong>GET</strong> 
* <strong>파일</strong> 등록 /files/{filename} -> <strong>PUT </strong>
* <strong>파일</strong> 삭제 /files/{filename} -> <strong>DELETE </strong>
* <strong>파일</strong> 대량 등록 /files -> <strong>POST</strong>

<br>

<strong>⭐️PUT - 신규 자원 등록 특징</strong>
* 클라이언트가 리소스 URI를 알고 있어야 한다. 
  * 파일 등록 /files/{filename} -> PUT 
  * PUT <strong>/files/star.jpg</strong>


* 클라이언트가 직접 리소스의 URI를 지정한다.


* 스토어(Store)
  * 클라이언트가 관리하는 리소스 저장소 
  * 클라이언트가 리소스의 URI를 알고 관리 
  * 여기서 스토어는 /files

<br>

### HTML FORM 사용
* HTML FORM은 <strong>GET, POST만 지원</strong> 
* AJAX 같은 기술을 사용해서 해결 가능 -> 회원 API 참고 
* 여기서는 순수 HTML, HTML FORM 이야기 
* GET, POST만 지원하므로 제약이 있음

<br>

<strong>API 설계 - HTML FORM 사용</strong>
* <strong>회원</strong> 목록 /members -> <strong>GET</strong>
* <strong>회원</strong> 등록 폼 /members/new -> <strong>GET</strong>
* <strong>회원</strong> 등록 /members/new, /members -> <strong>POST</strong>
* <strong>회원</strong> 조회 /members/{id} -> <strong>GET</strong>
* <strong>회원</strong> 수정 폼 /members/{id}/edit -> <strong>GET</strong>
* <strong>회원</strong> 수정 /members/{id}/edit, /members/{id} -> <strong>POST</strong>
* <strong>회원</strong> 삭제 /members/{id}/delete -> <strong>POST</strong>

<br>

<strong>정리</strong>
* HTML FORM은 <strong>GET, POST만 지원</strong>
* <strong>컨트롤 URI</strong> 
  * GET, POST만 지원하므로 제약이 있음 
  * 이런 제약을 해결하기 위해 동사로 된 리소스 경로 사용 
  * POST의 /new, /edit, /delete가 컨트롤 URI 
  * HTTP 메서드로 해결하기 애매한 경우 사용(HTTP API 포함)

<br>

### 참고하면 좋은 URI 설계 개념

https://restfulapi.net/resource-naming

* <strong>문서(document)</strong>
  * 단일 개념(파일 하나, 객체 인스턴스, 데이터베이스 row)
  * <em>Ex) /members/100, /files/star.jpg </em>


* <strong>컬렉션(collection)</strong>
  * 서버가 관리하는 리소스 디렉터리 
  * 서버가 리소스의 URI를 생성하고 관리 
  * <em>Ex) /members </em>


* <strong>스토어(store)</strong>
  * 클라이언트가 관리하는 자원 저장소 
  * 클라이언트가 리소스의 URI를 알고 관리 
  * <em>Ex) /files </em>


* <strong>컨트롤러(controller), 컨트롤 URI </strong>
  * 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행 
  * 동사를 직접 사용 
  * <em>Ex) /members/{id}/delete</em>

