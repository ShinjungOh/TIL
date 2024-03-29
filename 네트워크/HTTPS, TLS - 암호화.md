# HTTPS, TLS

## 암호화

![](../Images/암호화.png)

`https` 암호화된 http (HTTP + TLS)     
암호화는 승인된 당사자만 정보를 이해할 수 있도록 데이터를 `스크램블`한 방법  
이를 복호화하려면 송신자와 수신자가 서로 동의한 `키`가 필요   
이를 만들기 위해 키가 쓰이기도 함     

> `ciphertext` = `plaintext` + `key`

* ciphertext : 암호문 

![](../Images/TLS암호화.png)
![](../Images/https보안사진.png)

<br><br>

## 스크램블

각 단어나 문자를 패턴에 따라 암호화하는 것이 아니라, `무작위 방식`으로 개별 데이터 비트를 섞는 것

![](../Images/스크램블.png)

![](../Images/AES_algorithm.png)

공통 128비트 고급 암호화 표준(Advanced Encryption Standard, AES)으로 암호화된 파일의 경우   
이 파일을 구성하는 비트는 약 10회 스크램블되며, 다른 컴퓨터가 키 없이 해독하려면 아주 오랜 시간이 소요     
비트가 높아질수록 스크램블을 많이 하게 되고 더 복잡해짐   

128비트는 AES의 가장 약한 버전, 192비트 및 256비트 키 크기도 제공  

<br><br>

## 대칭 암호화

키를 하나만 사용하는 암호화 방법   
일반적으로 사용되는 대칭 암호화 알고리즘은 DES, AES 등

> **Ex. "hello"라는 텍스트를 키로 암호화할 경우**
> 
> 동일한 키로 암호를 해독해서 hello를 반환
> * **Plaintext + key = ciphertext:** hello + 2jd8932kd8 = X5xJCSycg14=    
> * **Ciphertext + key = plaintext:** X5xJCSycg14= + 2jd8932kd8 = hello   

<br><br>

## 비대칭 암호화 (공개키 암호화)

두 개의 다른 키(공개키, 개인키)로 데이터를 암호화하거나 서명하고, `공개 키`를 누구나 사용할 수 있도록 하는 방법       
공개키로 암호화된 데이터는 `개인키로만 복호화` 가능  
일반적으로 사용되는 비대칭 암호화 알고리즘은 RSA, DH(Die–Hellman) 등    

HTTPS를 가능하게 하는 프로토콜인 TLS는 부분적으로 비대칭 암호화를 사용(TLS1.3)  
비대칭 암호화로 인증을 한 후, 대칭 암호화로 보안적 통신을 시작      
`TLS 핸드셰이크 과정`에서 처음 인증할 때 비대칭 암호화를 하고   
그 이후 클라이언트와 서버는 `세션키`라고 하는 키를 기반으로 대칭 암호화를 기반으로 암호화된 통신을 함     

<br><br>

## 암호화의 필요성

암호화는 의도된 수신자 또는 송신자를 제외하고는 통신을 하이재킹하여 읽을 수 없도록 함  
민감한 `데이터의 유출을 방지`하고 `데이터 무결성을 보장`  

* 데이터 무결성 : 데이터의 정확성과 일관성  
* Ex. 신용카드 정보 등 
