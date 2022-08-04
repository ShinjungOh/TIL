# SVG

## Scalable Vector Graphics
웹 친화적인 벡터 파일 포맷  
* 확장 가능한 벡터 그래픽 
* XML 기반의 2차원 그래픽
* HTML 태그의 집합 => css와 javascript로 컨트롤 가능

<br><br>

## 장점
* 확대해도 이미지가 깨지지 않는다.
* 크기를 키워도 용량이 늘어나지 않는다.

<br><br>

## 단점
* 코드로 이루어져있기 때문에 복잡한 이미지일수록 파일 사이즈가 커진다.

<br><br>

## HTML에 SVG 적용하기
내부 요소 조작시 3, 4번 사용

<br>

### 1. img 태그로 사용
    src="" 속성값으로 svg 파일을 연결

<br>

### 2. css background로 사용
      background-image 속성값으로 svg 파일을 연결  
      background: url(img.svg)

<br>

### 3. 인라인으로 구현
    svg 파일의 코드를 그대로 html 코드 안에서 사용

* Tailwind CSS 에서 사용
   
<br>

### 4. object 태그 사용
```haml
<object data="./img.svg" type="image/svg+xml"></object>
```

<br><br>

## 웹사이트
> PNG SVG 변환 : https://convertio.co/kr/svg-png/