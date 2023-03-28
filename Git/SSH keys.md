# Github

## SSH(Secure Shell Protocol)

ID, password를 입력하지 않고도 커밋 가능
* 깃허브 프로필 -> Settings -> SSH and GPG keys -> New SSH key  
>https://docs.github.com/en/authentication/connecting-to-github-with-ssh

<br>

## SSH key 생성 및 Github 연결
1️⃣ **유저 이메일 찾기** 

```
git config --global user.email
``` 

<br>

2️⃣ **터미널에서 키 생성하기**

```
ssh-keygen -t rsa -C "user@email"
```

<br>

3️⃣ **기본 파일 위치 및 보안 암호 입력 : enter**

```
Enter file in which to save the key (`위치`): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
```

<br>

4️⃣ **Your public key has been saved in `경로`**

<br>

5️⃣ **cat `경로` 입력 후 뜨는 정보 복사**

<br>

6️⃣ **Github SSH keys / Add new**

```
title : 컴퓨터 이름 등 지정  
key : 복사한 내용 붙여넣기
```


