## LAN(Local Area Network)이란?
- LAN : 한정된 지역에서의 네트워크 구축
- WAN(Wide Area Network) : 멀리 떨어진 곳과의 네트워크 구축

## 데이터 네트워크는 이더넷과 토큰링 두가지 기억하기! 

### 이더넷 
- 프로토콜은 CSMA/CD (Carrier Sensor Multiple Access / Collison Detection) : 눈치껏 알아서 네트워크 통신
- 충돌이 일어난다면 랜덤한 시간만큼 대기하다가 다시 통신 시도
- 우리나라에서는 토큰링보다는 이더넷을 더 많이 사용 

### 토큰링
- 이더넷과 다르게 토큰을 가지고 있는 데이터만이 토큰을 획득한 순서대로 데이터 통신 가능
- 네트워크에 아무런 통신이 일어나지 않고 있어도 토큰이 없다면 통신 불가능 

### UTP, Unshield Twist Pair
- 두개가 한쌍
- 언쉴드, 감싸지 않음
### STP, Shield Twist Pair
- 토큰링에서 많이 쓰임

### 10 Base 5
- 10M 속도, 디지털 방식, 500m까지 전송 가능
- 아날로그 방식은 브로드밴드임
### 10 Base T
- 10M 속도, 디지털 방식, 케이블 종류 T 는 UTP 케이블

### 망분리 1.
- 보안때문에 네트워크를 서로 분리하는 것
- 물리적 망분리와 논리적 망분리가 있다.
  - 물리적 망분리는 망을 인터넷망과 업무망으로 나누는 것

### 맥 주소 (MAC Address, Media Access Control Address)
- 네트워크 상에서 통신시 서로를 구분하기 위한 주소
- ARP(Address Resolution Protocol) : IP 주소 -> MAC 주소 변환
- cmd > ipconfig/all -> 물리주소로 나오는 부분이 맥주소
- IP : 논리적, MAC Address : 물리적
- 브로드캐스트 : 같은 네트워크 상 모든 PC에 메시지 보내는 것
- 다른 네트워크상에 존재하는 PC와 통신할 때는 라우터 사용
- IP 주소가 있어도 통신에는 MAC 주소를 사용하고 IP 주소를 MAC 주소로 변환해주는 것이 ARP !!
- 맥주소는 48bit, 6옥텟  
  - 앞쪽 절반은 장비를 만든 회사의 고유 번호
  - 나머지 뒷쪽은 일련번호로 하여 장비의 고유 정보로 사용 
