## HTTP 메소드 - GET, POST

### HTTP 메소드 종류 
<strong>주요 메소드</strong>

* <strong>GET</strong> : 리소스 조회 
* <strong>POST</strong> : 요청 데이터 처리, 주로 등록에 사용 
* <strong>PUT</strong> : 리소스를 대체, 해당 리소스가 없으면 생성 (=폴더에 파일 덮어쓰기) 
* <strong>PATCH</strong> : 리소스 부분 변경 
* <strong>DELETE</strong> : 리소스 삭제

<br>

<strong>기타 메소드</strong>

* <strong>HEAD</strong> : GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환 
* <strong>OPTIONS</strong> : 대상 리소스에 대한 통신 가능 옵션(메소드)을 설명 (주로 CORS에서 사용) 
* <strong>CONNECT</strong> : 대상 자원으로 식별되는 서버에 대한 터널을 설정 
* <strong>TRACE</strong> : 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행

<em>CONNECT, TRACE는 거의 사용 X</em>

<br>

### GET

    GET /search?q=hello&hl=ko HTTP/1.1 
    Host: www.google.com

* 리소스 조회 
* 서버에 전달하고 싶은 데이터는 query(쿼리 파라미터, 쿼리 스트링)를 통해서 전달 
* 메시지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않음

<br>

### POST

    POST /members HTTP/1.1 
    Content-Type: application/json
    
    {
        "username": "hello", 
         "age": 20
    }

* 요청 데이터 처리 
* <strong>메시지 바디를 통해 서버로 요청 데이터 전달</strong> 
* 서버는 요청 데이터를 <strong>처리</strong> 
  * 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다. 
* 주로 전달된 데이터로 신규 리소스 등록, 프로세스 처리에 사용

<br>

### POST 요청 데이터 처리 예시

스펙: POST 메서드는 <strong>대상 리소스가 리소스의 고유한 의미 체계에 따라 요청에 포함된 표현을 처리하도록 요청</strong>합니다. (구글 번역) <br> 

예를 들어 POST는 다음과 같은 기능에 사용됩니다.

* HTML 양식에 입력된 필드와 같은 데이터 블록을 데이터 처리 프로세스에 제공
  * <em>Ex) HTML FORM에 입력한 정보로 회원 가입, 주문 등에서 사용</em>

* 게시판, 뉴스 그룹, 메일링 리스트, 블로그 또는 유사한 기사 그룹에 메시지 게시
  * <em>Ex) 게시판 글쓰기, 댓글 달기</em>

* 서버가 아직 식별하지 않은 새 리소스 생성
  * <em>Ex) 신규 주문 생성</em>

* 기존 자원에 데이터 추가 
  * <em>Ex) 한 문서 끝에 내용 추가하기</em>


<strong>정리: 이 리소스 URI에 POST 요청이 오면 요청 데이터를 어떻게 처리할지 리소스마다 따로 정해야 함 -> 정해진 것이 없음</strong>

<br>

### POST 정리

<strong>1. 새 리소스 생성(등록)</strong> <br>
* 서버가 아직 식별하지 않은 새 리소스 생성

<strong>⭐️2. 요청 데이터 처리</strong> <br>
* 단순히 데이터를 생성하거나, 변경하는 것을 넘어서 프로세스를 처리해야 하는 경우
* <em>Ex) 주문에서 결제완료 -> 배달시작 -> 배달완료 처럼 단순히 값 변경을 넘어 프로세스의 상태가 변경되는 경우</em> 
* POST의 결과로 새로운 리소스가 생성되지 않을 수도 있음
* <em>Ex) POST /orders/{orderId}/start-delivery <strong>(컨트롤 URI)</strong></em>

<strong>3. 다른 메서드로 처리하기 애매한 경우</strong>

* <em>Ex) JSON으로 조회 데이터를 넘겨야 하는데, GET 메서드를 사용하기 어려운 경우</em>
* 애매하면 POST