# github

## 오픈소스 프로젝트

### forking workflow
* fork : 나의 repository에 복사해오는 것
* PR(pull request) : 오픈소스 프로젝트에 제출 -> 승인, 거절 등 반응 
* rebase : 오픈소스 프로젝트와 sync해 최신 상태 유지
* merge PR

<br>

## github 프로젝트 내 PC로 옮기기
repository -> code 

* <strong>download</strong> : 현재 서버에 있는 버전의 코드가 다운로드 
* <strong>clone</strong> : 서버와 연동해 최신 커밋도 받아오기
* <em>기본적으로 서버에 있는 것의 이름은 origin이라고 설정되어 있다.</em>

<br>

## remote
* git clone URL  
* git remote -v : 모든 remote URL 보기 
* git remote add name URL : 현재 폴더에서 다른 깃허브 링크 추가
* git remote 
* git remote show 
* git remote show origin : 해당 정보 확인

<br>

## SSH(Secure Shell Protocol)
ID, password를 입력하지 않고도 커밋 가능
* 깃허브 프로필 -> 세팅 -> SSH and GPG keys

https://docs.github.com/en/authentication/connecting-to-github-with-ssh

<br>

## push
* git push
* git push -f : 서버에서 작업한 내용은 삭제되고 로컬 작업 내용으로 대체 (force)

<br>

## fetch
히스토리를 업데이트하지만, 작업환경 HEAD는 그대로 유지(로컬 master 브랜치) <Br>
서버에서 어떤 일이 발생하고 있는지, 누가 어떤 일을 했는지 확인할 때 주로 사용 

* git fetch : 서버의 모든 히스토리 가져오기(작업중인 HEAD는 유지)
* git fetch origin 
* git fetch origin master : 특정한(master) branch만 가져오기

<br>

## pull
서버의 히스토리를 가지고 오면서, 로컬의 내용을 함께 merge <br>
로컬 버전을 서버와 동일하게 만들 때 사용 (로컬 헤드와 서버 헤드가 동일)

* git pull : fetch + merge
* git pull --rebase : rebase (merge 대신)


