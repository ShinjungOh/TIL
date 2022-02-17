## HTTP 메소드 - PUT, PATCH, DELETE

### PUT

    PUT /members/100 HTTP/1.1 
    Content-Type: application/json
    
    {
        "username": "hello", 
        "age": 20
    }


<strong>리소스를 완전히 대체</strong>
* 리소스가 있으면 대체 (수정이 아니라 완전히 덮어쓰는 것)
* 리소스가 없으면 생성 
* 쉽게 이야기해서 덮어쓰기


<strong>⭐️클라이언트가 리소스를 식별</strong> 
  * 클라이언트가 리소스 위치를 알고 URI 지정 
  * POST와 차이점

<br>

### PATCH
리소스 부분 변경 <br>

<em>HTTP에서 PATCH를 받아들이지 못하는 경우에는 POST 사용</em>

<br>

### DELETE
    DELETE /members/100 HTTP/1.1 
    Host: localhost:8080

리소스 제거