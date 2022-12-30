# git

## gitignore

git, github에 올리고 싶지 않은 파일이나 폴더를 .gitignore 파일 안에 넣어둘 수 있음


### 예시 

* .idea
* /node_modules
* /build

<br><br>

## 사용 방법

1️⃣ 트래킹되는 파일의 트래킹을 중지하려면   
`git rm --cached .` (staging area -> working directory로 이동)

<br>

2️⃣ `git add .`

<br>

3️⃣ `git commit -m "feat: .gitignore 추가"`
