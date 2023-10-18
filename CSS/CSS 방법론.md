# CSS 방법론

## 지향점 

* 코드의 재사용성 증가
* 유지보수가 용이
* 확장 가능한 코드
* 클래스명만으로 의미를 유추할 수 있음 

<br><br>

## SMACSS

**S**calable and **M**odular **A**rchitecture for CSS  
확장 가능하며 모듈식 아키텍처를 위한 CSS 방법론

CSS에 대한 확장형 모듈식 구조(by Jonathan Snook)  
CSS의 프레임워크가 아닌 하나의 스타일 가이드

<br>

### 규칙 

1. **Base** : 기본적인 스타일 정의 (Reset, Default, Variable, Mixins)
2. **Layout** : 레이아웃과 관련된 스타일 정의
    * Class명에 suffix `l-`를 붙임 : `.l-fixed #content { }`
3. **Module(Components)** : 재사용 가능한 모듈 관련 스타일을 정의
    * Block, Element, Module
    * 재사용을 위해 id 셀렉터와 element를 사용하지 않음 
    * element 셀렉터를 사용해야 한다면 class를 이용한 child 셀렉터 사용 : `.box > span`
    * Ex) nav bar, 이미지 슬라이더, dialogs, widgets, tables, icons
4. **State** : 상태에 따른 스타일 변경
   * Class명에 suffix `is-` 또는 `s-`를 붙임
   * hover, active, focus, hidden, expend 등의 상태에서 사용
   * Ex) `class="btn btn_good is-active"`
5. **Theme** : 스타일 가이드에 따라 스타일을 수정
   * 페이지 전반적인 look and feel 제어
   * 색상이나 이미지를 불변하는 스타일과 분리, 기존 스타일을 재선언하여 사용할 수 있음 
   * 적용범위가 넓은 테마는 suffix `theme-`를 붙임 : `.theme-dark {}`

<br>

### SMACSS 주의점

* 파생된 CSS 셀렉터 사용금지
* ID 셀렉터 사용금지
* !important 사용 금지
* Class 이름은 의미있게, 다른 개발자가 이해할 수 있도록 선언


<br><br>

## 참고 사이트

> [CSS방법론](https://wit.nts-corp.com/2015/04/16/3538)  
> https://blog.logrocket.com/bem-vs-smacss-comparing-css-methodologies/  
> https://ko.learnlayout.com/  
