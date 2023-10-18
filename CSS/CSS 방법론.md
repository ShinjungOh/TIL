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

## BEM

**B**lock, **E**lement, **M**odifier  
CSS를 구조화하고 모듈화하는 방법론  

객체지향 프로그래밍 OOP(Object Oriented Programming)와 유사  
ID는 사용할 수 없고, 오직 class명만 사용 가능  
`.header__navigation‐‐secondary` 같은 class를 사용

<br>

### 장점 및 주의점

* 클래스 이름 만으로도 원하는 요소를 선택할 수 있음 -> 유지 보수성과 확장성 증가
* ⚠️ class명은 구체적이고 명료하여 HTML안에서도 읽기 쉬워야 함 
  * class명이 무엇을 나타내는지 분명하게 전달해야 함

<br>

### 규칙

1. **Block** : 독립적으로 존재할 수 있는 기본적인 컴포넌트, 문단 전체에 적용된 element 또는 element를 담고 있는 컨테이너
   * `.block`으로 명명
   * Ex) header, nav, logo, login form, menu, search from, content, footer, button 
2. **Element** : block 내부에서 특정 기능을 수행하는 컴포넌트, element는 상황에 따라 달라짐
   * `.block__element`로 명명 : `.header__menu {}`
   * 각 element는 두 개의 밑줄표시로 연결하여 block 다음에 작성
   * block__는 Block과 Element를 구분하는 구분자
3. **Modifier** : Block 또는 Element의 상태를 나타냄 
   * `.block--modifier`로 명명
   * block--는 Block과 Modifier를 구분하는 구분자
   * Ex) button의 상태 : primary, success, warning 등 

<br>

### 네이밍 컨벤션

```
Block    : .block {}
Element  : .block__element {}
Modifier : .block--modifier {}
.block__element--modifier {}
```

* block 이름이나 element 이름이 길 경우 – 하이픈으로 연결 : `.block-name__element-name`

<br>

### 예시

```html
<nav class="nav">
  <ul class="nav__list">
    <li class="nav__item">
      <a class="nav__link" href="/">Home</a>
    </li>
    <li class="nav__item nav__item--active">
      <a class="nav__link" href="/about">About</a>
    </li>
    <li class="nav__item">
      <a class="nav__link" href="/contact">Contact</a>
    </li>
  </ul>
</nav>
```

* Block : nav 
* Element : list, item, link 
* Modifier : item--active

<br><br>

## OOCSS

**O**bject **O**riented CSS  
CSS를 모듈 방식으로 코딩하여 중복을 최소화하는 기법   
CSS 코드를 재사용 가능한 모듈로 분리

<br>

### 장점 및 주의점

* 스타일 속성과 콘텐츠를 분리하여 작성
* 반복되는 패턴을 추상화하여 재사용 가능한 모듈로 분리
* 구체적인 스타일보다는 일반적인 스타일을 사용하여 모듈의 재사용성을 높임 

<br>

### 단점

* 다중 클래스 사용으로 HTML이 복잡해짐
* non-semantic한 클래스 사용
* Sass와 함께 사용하게 되면 단점을 보완할 수 있음

<br>

### 규칙

1. **Objects** : UI 요소의 일반적인 시각적 표현을 정의
   * Ex) button, input, list 등
2. **Components** : Objects를 조합하여 실제 UI 컴포넌트를 생성
   * Ex) header, footer, sidebar 등
3. **Modules** : Components를 조합하여 페이지를 만듦
   * Ex) home, about, contact 등

<br>

### 예시

#### Object: button

```html
<div class="button">Click Me</div>

.button {
    display: inline-block;
    padding: 10px 20px;
    background-color: #428bca;
    border-radius: 4px;
    color: #fff;
    text-decoration: none;
}
```

#### Component: header, nav, list, item, link

```html
<header class="header">
  <div class="logo">
    <img src="logo.png" alt="Logo">
  </div>
  <nav class="nav">
    <ul class="nav__list">
      <li class="nav__item">
        <a class="nav__link" href="/">Home</a>
      </li>
      <li class="nav__item">
        <a class="nav__link" href="/about">About</a>
      </li>
      <li class="nav__item">
        <a class="nav__link" href="/contact">Contact</a>
      </li>
    </ul>
  </nav>
</header>
```

<br><br>

## SMACSS, BEM, OOCSS 방법론 차이점

클래스 이름의 규칙, CSS구조에서 차이

* SMACSS : 스타일을 기능과 역할에 따라 분류, 5가지 범주인 Base, Layout, Module, State, Theme의 카테고리로 분류, 클래스 이름에 prefix를 사용해 의미를 명확하게 함
* BEM : CSS 클래스 이름을 사용해 요소를 나타냄, 각 요소는 Block, Element, Modifier 세 가지 형태로 모듈화
* OOCSS : CSS를 객체지향적으로 구현, 스타일과 레이아웃을 분리하고 스타일을 모듈화

<br><br>

## 참고 사이트

> [CSS방법론](https://wit.nts-corp.com/2015/04/16/3538)  
> https://blog.logrocket.com/bem-vs-smacss-comparing-css-methodologies/  
> https://ko.learnlayout.com/  
