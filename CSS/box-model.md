# CSS

## Box-Model

![](../Images/box-model.png)

* `content` : 요소의 실제 내용이 차지하는 영역
* `padding` : 내용과 테두리 사이의 간격, 내부 여백
* `border` : 내용과 패딩을 감싸는 테두리
* `margin` : 테두리와 이웃하는 요소 사이의 간격, 외부 여백
* `box-sizing` : 요소의 너비와 높이를 계산하는 방법을 지정

<br><br>

## box-sizing

기본값이 content-box라서 발생하는 오류가 많음  

![](../Images/css_box_sizing.png)

* content-box : Content 영역을 기준으로 box의 size를 적용, **⚠️기본값**
* border-box : Border 영역을 기준으로 box의 size를 적용 
  * 사람이 인식하는 박스 크기는 대개 border를 기준으로 함
  * content와 padding을 포함한 박스 크기
