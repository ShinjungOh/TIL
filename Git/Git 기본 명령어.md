# 기본 명령어

## add
<strong>로컬 파일 추가하기</strong> <br>

working directory의 untracked 카테고리에 있는 파일을 git이 트래킹할 수 있도록 
staging area에 옮길 때 사용

<br>

## ignore
Git, Github에 올리고 싶지 않은 파일을 git ignore 파일 안에 넣어둔다. <br>

트래킹되는 파일의 트래킹을 중지하려면 git rm --cached 사용 (staging area -> working directory로 이동)

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
