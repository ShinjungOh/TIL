## Git Workflow

### Git의 작업환경

<strong>Local</strong>
1. <strong>working directory</strong> : 프로젝트의 파일을 작업하는 곳
2. <strong>staging area</strong> : 버전 히스토리에 저장할 준비가 되어있는 파일을 옮겨놓는 곳 (add 명령어 사용)
3. <strong>.git directory(repository)</strong> : 버전의 히스토리를 가지고 있는 곳

<br>

<strong>흐름</strong> <br>

working directory에서 어느정도 준비가 된 파일 -> staging area로 이동 -> 
commit 명령어를 통해 git 버전 히스토리에 저장 (.git directory)

.git directory에 저장된 버전은 checkout 명령어를 통해 원하는 버전으로 다시 돌아갈 수 있다.

<br>

<strong>문제점과 해결방안</strong>
* Git 히스토리는 로컬(내 컴퓨터)에만 보관되기 때문에, 컴퓨터에 문제가 생기면 잃어버릴 수 있음


* Github 등의 서버에 push 명령어를 이용해 나의 git directory를 업로드
* 서버에서 로컬로 다운 시, pull 명령어 사용

<br>

### 버전에 담긴 정보
각각의 commit에는 고유한 해쉬코드가 부여된다. <br>
다음과 같은 정보를 알 수 있다.
* 아이디
* 버전 관련 메시지
* 작성자
* 날짜, 시간

<br>

### file status
<strong>working directory</strong>
* untracked : 아직 트래킹되지 않는 파일 카테고리 (새로 만들어진 파일, 기존에 존재하던 프로젝트에서 git 초기화 시)
* tracked : git이 트래킹하는 파일 카테고리
  * unmodified : 이전 버전과 비교해 수정되지 않은 파일
  * modified : 수정된 파일 (-> staging area로 이동 가능)




