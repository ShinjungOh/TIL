# undo

## restore
로컬에서 작업하는 staging area 또는 working direcory에서 작업하는 내용 초기화  

* git restore . : working directory 안의 모든 수정된 파일 초기화  
* git restore file.txt  
* git restore --staged file.txt : stage된 파일을 working directory로 가져오기
* git restore --source=hash file.txt 
* git restore --source=HEAD~2 file.txt : HEAD에서 2번째 떨어진 곳으로 특정 파일을 restore 
* git clean -fd 

<br>

## commit 
서버에 업로드 되지 않았을 때 사용 가능
* git commit --amend : 수정한 내용 업데이트
* git commit --amend -m "수정할 메시지" : 커밋 메시지 수정

<br>

## reset
특정한 커밋으로 모든 것을 초기화 
* git reset HEAD file.txt
* git reset --mixed HEAD : 버전 히스토리에서 커밋을 삭제하고, 작업 중인 내용은 working directory로 이동
* git reset --soft HEAD : 커밋을 삭제하고, 변경된 내용은 다시 staging area로 가져옴
* git reset --hard HEAD : 커밋을 삭제하고, 로컬에도 가져오지 않는다. (마지막 커밋 이후 수정한 모든 로컬 파일 초기화)

<br>

## reflog
reference log, 로그를 참조하다 <br>
이전에 HEAD가 가리키고 있었던 내용을 다 기억함으로써, 원하는 시점으로 돌아갈 수 있다. <br>
기존에 커밋을 해두었을 경우에 가능

* git reflog : 기존에 실행했던 명령어, 그것으로 인해 변경되었던 HEAD가 가리키고 있었던 포인트 확인 가능 
* git reset --hard hash : HEAD가 지정한 해시코드를 가리킴

<br>

### commit 하지 않은 경우?
커밋하지 않은 경우, 로컬에 작성한 것을 git reset hard 했다면
* local history 확장 프로그램 설치 
* 로컬에서 작업하는 파일 시간별로 히스토리 자동 저장