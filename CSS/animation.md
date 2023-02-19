# CSS

## animation

애니메이션이란 연속되는 이미지를 연결해서 자연스럽게 움직이는 것 처럼 보이게 만드는 기법

### 1. transition 속성 활용

변화 전, 후 관계를 부드럽게 이어주는 애니메이션  
transition은 **특정 이벤트를 기점(hover 등)** 으로 작동  
트리거가 필요

### 2. animation 속성과 keyframe 활용

시작하기 위한 이벤트가 필요 없음  
애니메이션의 시작, 정지, 반복까지 제어가 가능  
`@keyframes`로 애니메이션을 정의하고, 정의한 `애니메이션`을 불러와서 제어  
transition 보다 복잡함  

<br><br>

## @keyframes

CSS 애니메이션의 시작, 중간, 끝 등의 중간 상태를 정의

### from ~ to

```css
/* keyframe 작성 방법 */
@keyframes 애니메이션이름 {
	/* 시작 시점 css */
    from {
		left : 0;
	}
	/* 종료 시점 css */
	to {
		left : 200px;
	}
}
```

### 진행도(%) 표기

```css
/* keyframe 작성 방법 */
@keyframes 애니메이션이름{
	0% {
		left : 0;
	}
	50% {
		left : 200px;
	}
	100% {
		top : 200px;
		left : 200px;
	}
}
```

<br><br>

## animation 관련 속성

* `animation-name` : 어떠한 keyframes를 요소에 적용할 것인지 지정
* `animation-duration` : 애니메이션을 한 번 재생하는데 걸리는 시간을 설정
* `animation-direction` : 애니메이션 재생 방향을 정의 (정방향/역방향)
  * normal : 정방향으로 재생
  * reverse : 역방향으로 재생
  * alternate : 정방향으로 재생 (정방향/역방향을 번갈아 재생)
  * alternate-reverse : 역방향으로 재생 (역방향/정방향을 번갈아 재생)
* `animation-iteration-count` : 애니메이션 재생 횟수를 정의
  * 기본값 0 
  * infinite : 무한 반복
  * direction과 연관 
* `animation-timing-function` : 애니메이션 재생 패턴을 정의
  * transition-timing-function과 유사
* `animation-delay` : 애니메이션 시작을 얼마나 지연할 지 설정

<br><br>

## animation 단축속성

순서가 바뀔 경우 오류 발생

```
/* name duration timing-func. delay iteration-count direction */
animation: moveRight 0.4s linear 1s infinite alternate
```

