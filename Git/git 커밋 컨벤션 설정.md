# git 커밋 컨벤션 설정

## 커밋 메시지

태그와 제목으로 구성

`태그: 제목` 형태

* : 뒤에만 띄어쓰기

> `feat` : 새로운 기능 추가   
> `fix` : 버그 수정   
> `docs` : 문서 수정   
> `style` : 코드 포맷팅, 세미콜론 누락, 코드 변경이 없는 경우   
> `refactor` : 코드 리팩토링   
> `test` : 테스트 코드, 리팩토링 테스트 코드 추가   
> `chore` : 빌드 업무 수정, 패키지 매니저 수정

<br><br>

## 태그

### 기능

Feat, Fix, Design, !BREAKING CHANGE 태그

> `Feat`: 새로운 기능을 추가할 경우  
> `Fix`: 버그를 고친 경우  
> `Design`: CSS 등 사용자 UI 디자인 변경  
> `!BREAKING CHANGE`: 커다란 API 변경의 경우 (API의 arguments, return 값의 변경, DB 테이블 변경, 급하게 치명적인 버그를 고쳐야 하는 경우 등)

<br>

### 개선

Style, Refactor, Comment 태그

> `Style`: 코드 포맷 변경, 세미 콜론 누락, 코드 수정이 없는 경우 (오타 수정, 탭 사이즈 변경, 변수명 변경)  
> `Refactor`: 프로덕션 코드 리팩토링, 새로운 기능이나 버그 수정없이 현재 구현을 개선한 경우  
> `Comment`: 필요한 주석 추가 및 변경  

<br>

### 그 외

Docs, Test, Chore, Rename, Remove 태그

> `Docs`: 문서를 수정한 경우 (README.md 등)  
> `Test`: 테스트 추가, 테스트 리팩토링 (프로덕션 코드 변경 없음, test 폴더 내부의 변경이 일어난 경우)  
> `Chore`: 빌드 태스크 업데이트, 패키지 매니저 설정할 경우 (프로덕션 코드 변경 없음, package.json 변경, dotenv 요소 변경 등, 모듈 변경)  
> `Rename`: 파일 혹은 폴더명을 수정하는 경우  
> `Remove`: 사용하지 않는 파일 혹은 폴더를 삭제하는 경우  


<br><br>

## 커밋 메시지 이모지

<br>

| Emoji | Description                                    |
|:-----:|------------------------------------------------|
|  🎨   | 코드의 **형식 / 구조**를 개선 할 때                        |
|  📰   | **새 파일**을 만들 때                                 |
|  📝   | **사소한 코드 또는 언어**를 변경할 때                        |
|  🐎   | **성능**을 향상시킬 때                                 |
|  📚   | **문서**를 쓸 때                                    |
|  🐛   | **버그** reporting할 때, @FIXME 주석 태그 삽입           |
|  🚑   | **버그**를 고칠 때                                   |
|  🔥   | **코드 또는 파일 제거**할 때 , @CHANGED주석 태그와 함께         |
|  🚜   | **파일 구조를 변경**할 때 . 🎨과 함께 사용                   |
|  🔨   | 코드를 **리팩토링** 할 때                               |
|  💄   | **UI / style** 개선시                             |
|   ♿   | **접근성**을 향상시킬 때                                |
|  🚧   | **WIP**(진행중인 작업)에 커밋, @REVIEW주석 태그와 함께 사용      |
|  💎   | New **Release**                                |
|  🔖   | 버전 **태그**                                      |
|   ✨   | **새로운 기능**을 소개 할 때                             |
|  ⚡️   | 도입 할 때 이전 버전과 **호환되지 않는 특징**, @CHANGED주석 태그 사용 |
|  💡   | **새로운 아이디어**, @IDEA주석 태그                       |
|  🚀   | **배포 / 개발** 작업과 관련된 모든 것                       |

<br><br>

## 참고 사이트

> https://udacity.github.io/git-styleguide/   
> https://overcome-the-limits.tistory.com/entry/%ED%98%91%EC%97%85-%ED%98%91%EC%97%85%EC%9D%84-%EC%9C%84%ED%95%9C-%EA%B8%B0%EB%B3%B8%EC%A0%81%EC%9D%B8-git-%EC%BB%A4%EB%B0%8B%EC%BB%A8%EB%B2%A4%EC%85%98-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0
