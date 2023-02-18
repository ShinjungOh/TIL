# CSS

## position

HTML 요소가 배치되는 방식을 결정하는 속성

- static(기본값)
- relative
- absolute
- fixed
- sticky

position의 속성값에 따라 `top, left, bottom, right` 속성을 이용해 요소의 좌표값을 변경하는 방식이 달라짐  
* `top, left, bottom, right` : 해당 방향 기준으로 요소의 좌표값 변경

<br><br>

## position : static(기본값)

문서상 원래 있어야 하는 위치에 배치

️⚠️ top, left, bottom, right, z-index 속성 사용 불가  
위치 조정이 불가능한 기본 HTML 요소의 상태

<br><br>

## position : relative

`원래 있던 자리를 기준`으로 요소의 위치를 조정  
top, left, bottom, right 속성 적용 가능

<br><br>

## position : absolute

`절대 좌표를 기준`으로 요소의 위치를 조정    
top, left, bottom, right 속성 적용 가능

기준이 절대 좌표인 만큼, **절대 좌표의 기준이 되는 축**이 필요  
대상 요소의 부모 중 `relative가 적용된 요소`를 찾아서 **절대 좌표의 기준**으로 삼음  
상위와 그 상위에 모두 relative가 적용되어 있다면, `가장 가까운 상위의 relative 요소`를 기준으로 함  
relative가 적용된 요소가 없다면, `HTML의 바디 전체`를 기준으로 잡음  

<br><br>

## position : fixed

`viewport를 기준`으로 요소의 위치를 조정  
top, left, bottom, right 속성 적용 가능

스크롤과 무관하게 뷰포트를 기준으로 화면에 요소의 위치를 고정  

<br><br>

## position : sticky

`부모 요소의 좌표 기준` 으로 요소의 위치를 조정   
최근에 추가된 속성

스크롤을 내려가지 않았을 때는 static처럼 작동하다가,  
해당요소의 위치 아래로 스크롤이 내려가면 지정한 좌표에 fixed처럼 고정

<br><br>

## z-index

여러 요소가 겹쳐져 있을 때, 무엇이 앞으로 나올지 결정하는 속성  
숫자가 클수록 앞으로 나옴   

position을 이용해 요소의 위치를 옮기다 보면 여러개의 요소가 겹쳐지는 경우가 생기는데, 이럴 때 우선 순위를 정할 수 있음

```
z-index: auto (기본값)
z-index: 1
z-index: 9990
```
