# 기본 명령어

## add
<strong>로컬 파일 추가하기</strong> <br>

working directory의 untracked 카테고리에 있는 파일을 git이 트래킹할 수 있도록 
staging area에 옮길 때 사용

<br>

## ignore
Git, Github에 올리고 싶지 않은 파일을 .gitignore 파일 안에 넣어둔다. <br>

1️⃣ 트래킹되는 파일의 트래킹을 중지하려면 <br>
git rm --cached . 사용 (staging area -> working directory로 이동)

2️⃣ git add .

3️⃣ git commit -m "Apply .gitignore"

<br>

## status
<strong>작업 중인 상태 확인</strong>
* git status -help : 함께 실행할 수 있는 옵션 확인<br>
* git status : git status --long이 default 값  
* git status --short : 간단하게 확인

<br>

## diff
<strong>staging area와 working directory의 변경된 내용 확인</strong>
* git diff : working directory에 있는 것 비교 
* git diff --staged : staging area에 있는 것 비교
* git diff --cached : --staged 와 동일 

<br>

## commit
<strong>버전 등록하기</strong> <br>

staging area에 있는 변경사항을 git repository에 옮겨준다.
* git commit 
* git commit -m "Commit message" : 메시지와 함께 커밋
* git commit -am "Commit message" : 모든 파일을 메시지와 함께 커밋

<br>

### <strong>커밋할 때 팁</strong> <br>
* 작은 단위로 나누어 히스토리에 저장 
* 의미 있는 이름 지정
* 커밋 메시지에 해당하는 내용만 포함해 커밋

<br>

### 소스트리로 커밋하기
UI툴을 이용하면 세분화해서 조정할 수 있다.
* stage lines : 특정 라인만 staging area로 이동시킴
* stage hunk : 전체적인 블록을 staging 

<br>

### 파일 변경시 팁
* git rm : 파일 삭제시, 삭제 내역이 staging area에 자동 포함 
* git mv : 파일 이름 변경시, 변경 내역이 staging area에 자동 포함 

<br>

## log
<strong>버전 목록 보기</strong>

* git log : 커밋 리스트 보기
* git log --patch : 수정된 파일의 내용 확인
* git log -p : --patchd 와 동일  
* git log --oneline : 해쉬코드 앞자리 문자열과 커밋 메시지 확인
* git log --oneline --reverse : 오래된 순으로 확인

<br>

### HEAD 
내가 바라보는 현재 시점의 버전 <br>
언제든 원하는 시점으로 돌아갈 수 있다.

> `a` <- `b` <- `c` <- `d` <= `master`<br>
> `a : head~3`   `d : head`
 
* head~1 : 현재 헤드의 이전 버전
* head~2 : 현재 헤드의 이전 이전 버전

<br>

### 로그 꾸미기
* git log --pretty=oneline : --oneline과 동일
* git log --pretty=format:"%h - %an %ar %s" : 
* 포맷 공유
  * git log --graph --all --pretty=format :'%C(yellow)[%ad]%C(reset) %C(green)[%h]%C(reset) | %C(white)%s %C(bold red){{%an}}%C(reset) %C(blue)%d%C(reset)' --date=short

<br>

### 로그 심화 내용
* git log -2 : 최근 n개의 커밋 
* git log --author="ellie"
* git log --before="2020-09-29"
* git log --after="one week ago"
* git log --grep="message" : 커밋 메시지 중에서 찾기 
* git log -S="code" : 코드 안에서 찾기 
* git log file.txt

<br>

## tag
<strong>특정 커밋을 북마크</strong> <br>

대개 릴리즈 버전 태그

* git tag v1.0.0  
* git tag v1.0.0 hash : 특정 커밋에 태그 추가
* git show v.0.0 : 작성자, 작성일자, 메시지 등 정보 확인
* git tag -a v.1.0.0 -m "message" : 메시지 추가 
* git tag : 모든 태그 보기
* git tag -l "v1.0.*" : 특정 태그 보기
* git tag -d v1.0.0 : 태그 삭제

<br>

### semantic versioning
> ### v2.0.1<br>
> major : 2, 전체적인 업데이트 발생시<br>
> minor : 0, 작은 기능 업데이트, 개선시<br>
> fix : 1, 기존 기능에서 오류수정, 성능개선시