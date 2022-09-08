# Next.js Image Component

## Image

* resizing : 반응형 
* lazy load : 뷰포트에 들어올 때 로드
* 최적화 : webp 형식(Web을 위해서 만들어진 효율적인 이미지 포맷)
* CLS를 최대한 없애는 것이 목적

<br><br>

## CLS
누적 레이아웃 이동 (Cumulative Layout Shift)  
파일의 사이즈를 예측하고 미리 레이아웃을 잡아놓는 기능  
컴포넌트에 변경이 있으면 DOM 트리의 컴포넌트가 re-render -> ⚠️ 최적화에 반대됨  

<br><br>

## 참고 사이트
> https://nextjs.org/docs/api-reference/next/image  
> `webp` https://developers.google.com/speed/webp  
> `CLS` https://web.dev/i18n/ko/cls/
