# linux tree

## tree

디렉토리 구조를 표시해주는 명령어  
깃허브 리드미 등에 활용 가능

<br><br>

## 사용 방법

### depth 제한

`tree -L 2`  
depth 값으로 2를 주고 실행한 결과 출력  

* L : Level의 줄임말

```md
sjoh@SJOH-MacBookPro TIL % tree -L 2
.
├── CS
│   ├── 기본
│   └── 디자인패턴
├── CSS
│   ├── SVG.md
│   ├── Tailwind CSS.md
│   ├── flex.md
│   ├── styled-components textarea 태그 rows, cols 속성.md
│   ├── styled-components 스크롤바 스타일 적용.md
│   ├── styled-components.md
│   └── 우선순위 적용.md
├── Git
│   ├── Git Hooks.md
│   ├── Git Workflow.md
│   ├── Git 기본 명령어.md
│   ├── Git과 Github.md

13 directories, 223 files
```

<br>

### directory 이름만 표시

`tree -L 2 -d`

* -d : 디렉토리만 표시

```md
sjoh@SJOH-MacBookPro TIL % tree -L 2 -d
.
├── CS
│   ├── 기본
│   └── 디자인패턴
├── CSS
├── Git
├── Images
├── JavaScript
├── React
├── TypeScript
├── WebAPI
├── 네트워크
├── 알고리즘
└── 자료구조

13 directories
```

<br>

### 특정 폴더 제외

`tree -N -L 2 -d -I "node_modules|tests"`    
tests와 node_modules 폴더를 제외하는 경우

* -I : 특정 폴더를 제외할 경우 -I 뒤에 제외할 패턴을 입력
* -N : -N 옵션을 추가하면 한글의 깨지는 글자가 제대로 표시됨

<br><br>

## 참고 사이트 

> https://www.lesstif.com/lpt/linux-tree-54952142.html
