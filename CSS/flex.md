# CSS

## Flex
자신의 컨테이너가 차지하는 공간에 맞추기 위해 크기를 키우거나 줄이는 방법을 설정하는 속성  
`flex-grow`, `flex-shrink`, `flex-basis`    
flex 값에는 auto, initial, none, 단위 없는 양수 사용(비율)

<br><br>

## 속성

### `flex-grow`

유연하게 늘리기  
아이템이 flex-basis의 값보다 **커질 수 있는지**를 결정하는 속성  
container 요소 내부에서 할당 가능한 공간 선언  
`생략 시 기본값 0` => 따로 적용하기 전까지는 아이템이 늘어나지 않음

<br>

### `flex-shrink`

유연하게 줄이기  
아이템이 flex-basis의 값보다 **작아질 수 있는지**를 결정하는 속성  
container 요소 내부에서 item 요소의 크기 축소  
`생략 시 기본값 1` => 따로 적용하지 않아도 아이템이 flex-basis보다 작아질 수 있음 

<br>

### `flex-basis`

플렉스 아이템의 **기본 크기** 지정  
flex-direction이 row일 때는 너비, column일 때는 높이  
`생략 시 기본값 auto`

* 기본값 auto : 해당 아이템의 width 값 사용 
* width를 따로 설정하지 않을 경우 : 컨텐츠의 크기  
* content : 컨텐츠의 크기, width를 따로 설정하지 않은 경우와 동일 

<br><br>

## 사용법

### 순서

```
flex-grow, flex-shrink, flex-basis
```

<br>

### `값이 1개일 때`

* number를 지정하면 **flex-grow**
  * flex: 2;
* length 또는 percentage를 지정하면 **flex-basis**
  * flex: 10em;  
    flex: 30%;
* none, auto, initial 중 하나 지정

<br>

### `값이 2개일때`

* 첫 번째 값은 number이고, **flex-grow** 
* 두 번째 값은 다음 중 하나
  * number를 지정하면 **flex-shrink**
    * flex: 2 2;
  * length, percentage, auto를 지정하면 **flex-basis**
    * flex: 1 30px;

<br>

### `값이 3개일 때`

* **flex-grow**에 사용할 number
* **flex-shrink**에 사용할 number
* **flex-basis**에 사용할 length, percentage, auto
  * flex: 2 2 10%;

<br><br>

## 참고 사이트

> https://developer.mozilla.org/ko/docs/Web/CSS/flex  
> https://studiomeal.com/archives/197
