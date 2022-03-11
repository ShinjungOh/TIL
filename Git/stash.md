# stash

## stash란?

git history에 저장하지 않고도 작업하는 내용을 잠시 저장해둘 수 있다.
* 브랜치 전환시
* 다른 시도를 할 때 다른 작업을 잠시 저장해둘 경우

<br>

## Saving
* git stash push -m "message" : 새로운 stash 생성
* git stash : 아무 타이틀 없이 저장
* git stash --keep-index : stash에 저장하면서, 파일은 그대로 staging area에 두기
* git stash -u : 아직 트래킹되지 않은 파일들도 stash에 포함 (--include-untracked)

<br>

## Listing
* git stash list : 모든 stashe 보기 
* git stash show hash : 특정 stash 보기 
* git stash show hash -p : 특정 stash detail 보기  

<br>

## Applying
* git stash apply hash : 특정 stash 적용 
* git stash apply : 가장 최신 stash 적용 
* git stash pop : 가장 위에 있는 것이 working directory로 옮겨짐  
* git stash branch branchName : 새로운 브랜치가 만들어지면서 stash 적용 

<br>

## Deleting
* git stash drop hash : 특정 stash 삭제 
* git stash clear : 모든 stash 삭제