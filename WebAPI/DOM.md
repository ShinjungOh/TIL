# DOM

## DOM
Document Object Model <br>

![](../Images/DOM-model.png)

* 브라우저가 HTML 파일을 읽으면서 DOM 트리로 변환 
* 브라우저가 이해할 수 있는 오브젝트 트리로 만듦

<br>

>**DOM**
https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction

>**DOM API**
https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API

<br><br>

## Node
DOM Node 인터페이스는 DOM API를 사용하는 데에 필수

    EventTarget <- Node (모든 노드는 이벤트 타겟이다)


<br>

<strong>EventTarget</strong>
* addEventListener
* removeEventListener
* dispatchEvent

<br>

>**Node**
https://developer.mozilla.org/en-US/docs/Web/API/Node

>**Event Target**
https://developer.mozilla.org/en-US/docs/Web/API/EventTarget

<br><br>

## CSSOM
CSS Object Model <Br>

`DOM` + `CSS` = `CSSOM` <br>

브라우저가 HTML 파일을 DOM으로 만들었다면,
모든 스타일 정보를 종합해서 (DOM+CSS) CSSOM을 만든다. <br>

CSSOM에서는 사용자가 정의한 스타일, 브라우저에서 기본적으로 설정된 속성값들이 정의됨 (compute styles)

<br>

### Render Tree
최종적으로 브라우저에 표시될 내용만 선별되어 표기

`DOM` + `CSSOM` = `Render Tree` <br>

* <em> display가 none으로 설정되어 있다면 render tree에 포함되지 않는다. </em>

<br>

>**CSSOM**
https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model