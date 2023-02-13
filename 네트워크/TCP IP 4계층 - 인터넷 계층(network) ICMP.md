# TCP/IP 4계층 

## 인터넷 계층(network)

IP, ICMP, ARP가 대표적  
한 노드에서 다른 노드로 전송 계층에서 받은 세그먼트 또는 데이터그램을 패킷화해서 전송  

<br><br>

## ICMP

ICMP(Internet Control Message Protocol)는 노드와 노드 사이에서 **통신이 잘 되는지를 확인**할 때 쓰는 프로토콜
⚠️ 데이터를 교환하는데는 사용되지 않는 프로토콜  


일반적으로 테스팅에 사용  
IP와는 달리 TCP 또는 UDP와 같은 전송 계층 프로토콜과 연관되지 않고 **독립적**인 비연결형 프로토콜  
ICMP는 비연결형 프로토콜을 기반으로 구축됨


### 테스팅 예시 

```
ping www.google.com
```

ICMP 프로토콜을 기반으로 테스팅하는 것을 확인

<br><br>
