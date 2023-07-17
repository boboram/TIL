# Part-03. TCP/IP와의 만남 

- 60~83page

## TCP/IP, Transmission Control Protocol / Internet Protocol
- 인터넷을 사용하기 위한 프로토콜
- 각각의 네트워크에 접속되는 호스트들은 고유의 주소(NIC)를 가지고 있어서 자신이 속해 있는 네트워크 뿐만 아니라 다른 네트워크에 연결되어 있는 호스트까지도 서로 데이터를 주고받을 수 있도록 만들어져 있는 것이 특징
- 우리가 모르는 사이에 이미 컴퓨터에 TCP/IP는 세팅되어 있다.
- ‘/‘로 표현하는 이유? -> 2개의 프로토콜을 묶어서 표현하기 위함
    - TCP : 전송계층
    - IP : 인터넷 계층 

## IP, Internet Protocol
- 인터넷을 사용하는 우리에게 모두 하나씩 주어진 주소(나만을 위한 유일한 것‼️)
- 전 세계적으로 유일한 주소
- 공인 IP가 부족해지면서 비공인 주소를 사용할 수 있는 기술이 개발되고 있다.
    - NAT(Network Address Translation) : 사설망에선 비공인 IP를 사용하다가 외부와 연결해야 하는 경우 공인 IP를 사용
    - PAT : 동일 IP + 포트 번호만 변경
- NIC(Network Information Center) : 전 세계에서 공인 주소를 나눠주고 관리해주는 기관 
- IP 생김새 : 10.139.4.36
    - IPv4 : 32비트, 2의 32승개의 IP 보유
    - 이진수(0,1), 표현만 십진수(사람들의 이해를 쉽게 하기 위함)
    - IPv4가 고갈되면서 IPv6 등장(2의 128승개)
    - 이진수->십진수 변환, 십진수->이진수 변환, Logical And(둘다 1인 경우만 1) 기억하기

## DHCP(Dynamic Host Configuration Protocol)
- PC 하나하나마다 IP를 지정하는 것이 아니라 DHCP 서버가 IP주소를 모두 가지고 있다가 IP주소 요청시 자동으로 분배후 사용 완료하면 회수 

## 망분리 2
- 물리적 망분리 : 실제로 망이 2개(업무망, 인터넷망)
- 논리적 망분리 : 실제론 하나의 망을 사용하지만 두개를 쓰는 것처럼 사용
    - CBC(Client Based Computing) 방식 : PC기반(클라이언트) 가상화 
    - SBC(Server Based Computing) 방식 : 서버 기반 가상화 
