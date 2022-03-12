# undo

## restore
로컬에서 작업하는 staging area 또는 working direcory에서 작업하는 내용 초기화  

* git restore . : working directory 안의 모든 수정된 파일 초기화  
* git restore file.txt  
* git restore --staged file.txt : stage된 파일을 working directory로 가져오기
* git restore --source=hash file.txt 
* git restore --source=HEAD~2 file.txt : HEAD에서 2번째 떨어진 곳으로 특정 파일을 restore

<br>

## commit 
서버에 업로드 되지 않았을 때 사용 가능
* git commit --amend : 수정한 내용 업데이트
* git commit --amend -m "수정할 메시지" : 커밋 메시지 수정