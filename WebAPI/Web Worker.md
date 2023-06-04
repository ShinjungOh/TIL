# Web Worker

## 브라우저의 스레드 

자바스크립트는 싱글 스레드로 동작  
브라우저는 싱글 스레드로 동작하지 않음   
브라우저에서 처리되는 네트워크 통신이나 I/O(input/output)들은 서로 다른 스레드에서 동작

브라우저는 `메인 스레드`를 사용하여 웹 페이지의 모든 JavaScript를 실행하고 페이지 렌더링 및 가비지 수집 등의 작업을 수행   
과도한 JavaScript 코드를 실행하면 `기본 스레드가 차단`되어 브라우저의 작업을 지연시킬 수 있음   

![](../Images/webworker2.png)

<br><br>

## Web Worker 

웹사이트를 개선할 수 있는 방법   
웹 워커(Web worker)는 스크립트 연산을 웹 어플리케이션의 주 실행 스레드와 분리된 별도의 `백그라운드 스레드`에서 실행할 수 있는 기술  

이벤트 루프를 막을 우려가 있는 무거운 연산은 웹 워커를 사용해 처리할 수 있음  
웹 워커를 사용하면 메인 스레드와 별도의 `백그라운드 스레드`에서 코드를 병렬적으로 실행할 수 있음  
주 스레드(보통 UI 스레드)가 멈추거나 느려지지 않고 동작 가능  

![](../Images/webworker.png)

<br><br>

## 웹 워커 vs 서비스 워커

### 공통점

* [Web API](https://developer.mozilla.org/ko/docs/Web/API) 중 하나
* 웹 사이트에서 사용할 수 있는 워커 
* 둘 다 보조 스레드에서 실행되므로 기본 스레드와 사용자 인터페이스를 차단하지 않고 JavaScript 코드를 실행
* Window 및 Document objects에 대한 액세스 권한이 없으므로, DOM과 직접 상호 작용할 수 없으며 브라우저 API에 대한 액세스가 제한됨 

<br>

### 차이점 

|         |        웹 워커         |                         서비스 워커                         |
|:-------:|:-------------------:|:------------------------------------------------------:|
|   수명    | 웹 워커가 속한 탭과 밀접하게 연결 |                          독립적                           |
| 탭 종료 시  |         종료됨         |                    백그라운드에서 계속 실행 가능                    |
|   갯수    |    여러 웹 워커 생성 가능    |                  등록된 범위의 모든 활성 탭을 제어                   |
| 네트워크 요청 |          -          | 네트워크 요청을 가로챔(fetch이벤트를 통해),<br/>백그라운드에서 푸시 API 이벤트를 수신 |

* 웹 워커의 수명은 웹 워커가 속한 탭과 밀접하게 연결되어 있는 반면, 서비스 워커의 수명 주기는 독립적  
웹 워커가 실행 중인 탭을 닫으면 종료되지만, 서비스 워커는 사이트에 열려 있는 활성 탭이 없는 경우에도 백그라운드에서 계속 실행 가능
* 페이지는 여러 웹 워커를 생성할 수 있지만, 단일 서비스 워커는 등록된 범위의 모든 활성 탭을 제어
* 웹 워커와 달리 서비스 워커를 사용하면 fetch이벤트를 통해 네트워크 요청을 가로채고,  
백그라운드에서 push이벤트를 통해 Push API 이벤트를 수신

<br><br>

## 특징

* 웹 워커로 생성한 스레드는 브라우저 렌더링 같은 메인 스레드의 작업을 방해하지 않고, 새로운 스레드에서 스크립트를 실행
* 메인 스레드와 메시지를 교환할 수 있긴 하지만, 웹 워커엔 `메인 스레드와 연관 없는` 고유한 변수들과 자체 이벤트 루프가 존재  
* 웹 워커는 `DOM에 접근할 수 없`기 때문에 여러 CPU 코어를 동시에 사용해야 하는 연산에 주로 사용  
* 웹 워커 스레드 내에서 에러가 발생하면, 메인 스레드까지 전파되지 않음

<br><br>

## 종류

웹 워커는 2가지 타입이 존재

1. 전용 워커 Dedicated Worker : 처음 생성한 스크립트에서만 사용
   * new Worker 로 생성한 Worker 는 Dedicated Worker 이며, 부모 자식 간의 스레드끼리만 메시지 교환이 가능    
2. 공유 워커 [Shared Worker](https://developer.mozilla.org/ko/docs/Web/API/SharedWorker) : 여러 스크립트에서 사용 
   * Shared Worker 는 Worker 가 동일한 도메인 내에 존재하는 여러 스레드에서 사용이 가능하며, Port를 이용해 통신 

<br><br>

## 참고 사이트

> https://ko.javascript.info/event-loop  
> https://developer.mozilla.org/ko/docs/Web/API/Web_Workers_API  
> https://developer.mozilla.org/ko/docs/Web/API/Service_Worker_API  
> https://web.dev/workers-overview/  
> https://pks2974.medium.com/web-worker-%EA%B0%84%EB%8B%A8-%EC%A0%95%EB%A6%AC%ED%95%98%EA%B8%B0-4ec90055aa4d