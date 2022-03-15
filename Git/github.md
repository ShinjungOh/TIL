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

### remote
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
