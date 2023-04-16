# git fork

## 📌 Local & Remote

* Local : 로컬 기기(컴퓨터 등)에 존재하는 모든 Repository
* Remote : 원격 저장소(Github)에 존재하는 모든 Repository

<br>

### push, pull

`push`, `pull`을 통해 서로의 데이터를 주고받음 

* push : Local ➡️ Remote 업로드
* pull : Remote ➡️ Local 다운로드 

<br><br>

## 📌 Origin, Upstream & Downstream

### origin

깃허브에 존재하는 repository(remote)    
remote에 origin이라는 이름을 붙인 것

* 깃허브에서 repo 생성 시
* 깃허브에서 repo clone 시

<br>

### Upstream

* origin : upstream
* local : downstream 

push와 pull을 기준으로 생각했을 때 `origin`에서 ➡️ `local`로 흐르는 관계이기 때문

#### Upstream 설정하기 

```
git push -u origin main
```

* -u : --set-upstream, upstream 설정 옵션 

upstream을 한 번 설정하고 나면 `git push`, `git pull`만 입력해도 자동으로 origin의 main 브랜치로부터 push와 pull을 진행  
upstream 옵션을 통해 해당 브랜치에서 upstream과 downstream 관계가 설정됐기 때문

<br><br>

## 📌 Fork

* 내가 포크한 remote : origin
* 원본 remote repo : upstream 

> ⚠️ fork를 했을 때 혼란스러운 부분 
> 
> local과 origin의 관계에선 origin이 upstream, local이 downstream    
> fork한 repository를 기준으로 보면 origin이 downstream, 원본 remote가 upstream 

<br><br>

## 참고 사이트 

> https://pers0n4.io/github-remote-repository-and-upstream/
