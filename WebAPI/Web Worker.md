# Web Worker

## 브라우저의 스레드 

자바스크립트는 싱글 스레드로 동작  
브라우저는 싱글 스레드로 동작하지 않음   
브라우저에서 처리되는 네트워크 통신이나 I/O(input/output)들은 서로 다른 스레드에서 동작

![](../Images/webworker2.png)

<br><br>

## Web Worker 

웹 워커(Web worker)는 스크립트 연산을 웹 어플리케이션의 주 실행 스레드와 분리된 별도의 `백그라운드 스레드`에서 실행할 수 있는 기술  

이벤트 루프를 막을 우려가 있는 무거운 연산은 웹 워커를 사용해 처리할 수 있음  
웹 워커를 사용하면 메인 스레드와 별도의 `백그라운드 스레드`에서 코드를 병렬적으로 실행할 수 있음  
주 스레드(보통 UI 스레드)가 멈추거나 느려지지 않고 동작 가능  

![](../Images/webworker.png)

<br><br>

## 특징

* 웹 워커로 생성한 스레드는 브라우저 렌더링 같은 메인 스레드의 작업을 방해하지 않고, 새로운 스레드에서 스크립트를 실행
* 메인 스레드와 메시지를 교환할 수 있긴 하지만, 웹 워커엔 `메인 스레드와 연관 없는` 고유한 변수들과 자체 이벤트 루프가 존재  
* 웹 워커는 `DOM에 접근할 수 없`기 때문에 여러 CPU 코어를 동시에 사용해야 하는 연산에 주로 사용  
* 웹 워커 스레드 내에서 에러가 발생하면, 메인 스레드까지 전파되지 않음

<br><br>

## 종류

웹 워커는 2가지 타입이 존재

1. Dedicated Worker : 처음 생성한 스크립트에서만 사용
   * new Worker 로 생성한 Worker 는 Dedicated Worker 이며, 부모 자식 간의 스레드끼리만 메시지 교환이 가능    
2. Shared Worker : 여러 스크립트에서 사용 
   * Shared Worker 는 Worker 가 동일한 도메인 내에 존재하는 여러 스레드에서 사용이 가능하며, Port를 이용해 통신 

<br>

## 참고 사이트

> https://ko.javascript.info/event-loop  
> https://developer.mozilla.org/ko/docs/Web/API/Web_Workers_API  
> https://web.dev/workers-overview/  
> https://pks2974.medium.com/web-worker-%EA%B0%84%EB%8B%A8-%EC%A0%95%EB%A6%AC%ED%95%98%EA%B8%B0-4ec90055aa4d
