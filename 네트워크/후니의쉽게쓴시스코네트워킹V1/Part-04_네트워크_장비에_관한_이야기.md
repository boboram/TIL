# Part 04 네트워크 장비에 관한 이야기

## NIC, Network Interface Card
- 랜카드, 랜에 접속하기 위한 카드 
- 유저의 데이터를 케이블에 실어서 허브나 스위치, 라우터 등으로 전달해주고 자신에게 온 데이터를 CPU에게 전달
- 자신의 PC에 맞는 LAN카드를 골라야 하고, PC의 버스 방식도 고려해야 함
  - 버스 : 데이터가 날아다니는 길
- 우리가 사무실에서, 그리고 PC방에서 인터넷을 쓰고, 메일을 보내고, 온라인 게임을 할 수 있는건 PC 안에 랜카드가 존재하기 때문

## 망분리 3
- 물리적 망분리 : 2개의 망으로 업무용, 인터넷망 분리
- 논리적 망분리 : 1개의 망 사용
  - SBC(Server Based Computing) : 가격이 비싸지만 보안에 유리
  - CBC(Client Based Computing) : 가격이 저렴하고 따로 구축하지 않아도 되지만 보안에 취약

## 허브, Hub
- 같은 허브에 연결된 PC끼리는 통신이 가능
- 이더넷용, 토큰링용 방식이 있고 이더넷용을 주로 사용
  - 이더넷용이다?
    - CSMA/CD(Carrier Sense Multiple Access / Collision Detection ==> 적당히 눈치껏 알아서)
    - `같은 허브안에 있다 == 같은 콜리전 도메인이다 == 하나의 충돌 발생시 허브 안 모든 PC에 영향이 간다.`
    - 허브에 연결된 PC의 수가 많아질 수록 콜리전 도메인도 커진다.
- 허브는 보통 100미터까지 통신이 가능하고 그 이상으로 통신하기 위하여 증폭기인 리피터를 사용한다.
- 허브의 종류에는 NMS(네트워크 관리 시스템) 존재 여부에 따라 더미허브(NMS X), 인텔리전트허브(NMS ⭕)가 있다.

## 스태커블(Stackable), 스탠드얼론(Standalone)
- 스태커블 : 스택(쌓아두기) 가능, 여러대 허브 사용시  
- 스탠드얼론 : 단독 사용, 저렴, 작은 규모에서 사용

## 스위치
- 스위치 이더넷
  - 허브는 shared 이더넷
- 브리지가 원조임
- 콜리전 도메인을 나눠주기 위해 중간에 다리를 놓는 것
![image](https://github.com/boboram/TIL/assets/14108487/11e989fa-5a2f-4ba6-b991-9a705c39f140)
- 1번과 2번 사이에서 통신이 일어나면 나머지 모든 PC들은 기다려야만 하는 허브와는 달리 다른 PC들도 동시에 통신이 가능
- 여러개의 노드에서 **동시** 통신이 가능

### 허브 vs 스위치
- 허브가 스위치에 비해 가격이 저렴하고 데이터 전송 속도가 빠르다.
- 그 네트워크에서 어떤 데이터가 돌아다니느냐? 가 중요한 문제
  - 단순히 채팅, 메일과 같이 트래픽이 적다면 허브가 유리하다.
- 요즘은 스위치 가격이 저렴해지고 네트워크 사용자들이 모두 인터넷을 사용해서 많은 데이터를 주고받는 추세이기에 스위치가 각광받고 있음
- 브리지 테이블을 보면서 통신이 다리 한쪽에서만 일어나면 다리를 못 건너가게 하고 통신이 다리를 통과해야 가능하면 그때만 다리를 건너게 해준다.

## 브리지 / 스위치 기능
![image](https://github.com/boboram/TIL/assets/14108487/4a78bd15-5b2b-46d0-ae38-4eb55914635b)
- Learning, 배운다.
- Flooding, 모르면 들어온 포트를 제외한 모든 포트로 뿌린다. 
- Forwarding, 해당 포트로 건네준다. 
- Filtering, 출발지 세그먼트와 목적지 세크먼트가 동일한 경우 다른 포트로는 못 건너가게 막는다.
- Aging, 나이를 먹는다.

## 브리지 / 스위치 차이점
- 브리지가 스위치보다 더 저렴하다.
- 브리지는 소프트웨어적으로 프레임을 처리하고 스위치는 하드웨어로 프레임을 처리하기에 스위치가 좀 더 속도면에서 빠르다.
- 스위치가 제공하는 포트수가 더 많다.
- 스위치는 Cut-through, Store-and-forward 방식을 지원하지만 브리지는 Store-and-forward만을 지원한다.
  - Store-and-forward : 프레임 저장 후 처리, 오류 발생 시 유리
  - Cut-through : 목적지 주소만 본 후 바로 전송 처리, 48비트
  - Fragment-free : 처음 512비트를 보며(Store-and-forward장점) + 전체 프레임이 다 들어올 때까지 기다릴 필요가 없다.(Cut-through 장점)

## 브리지 / 스위치 에서 발생되는 루핑, 그리고 해결법(스패닝트리알고리즘) 

### 루핑
- 브리지나 스위치에 목적지까지의 경로가 두 개 이상 존재하면 발생하는 것
  - 양쪽 브리지를 통해 네트워크를 뱅뱅 돌게 됨 -> 루핑 발생
- 이더넷(CSMA/CD) 의 특성 : 하나씩만 데이터 전송 가능
- 이를 해결하기 위한 알고리즘이 스패닝트리알고리즘

### 스패닝트리알고리즘 
- 루핑을 미리 막기 위해 두 개 이상의 경로가 발생하면 하나를 제외하고 나머지 경로를 **자동으로 막아두었다가** 기존 경로에 문제가 생기면 막아놓은 경로를 풀어서 데이터를 전송하는 알고리즘
- **두 개의 링크 중 하나를 끊어 놓은 것**

## 폴트톨러런트, 로드밸런싱은 다른 개념! 
- 폴트톨러런트(Fault Tolerant) : 장애 대비책, 하나의 라우터가 죽으면 자동으로 대기하고 있던 대비책(라우터)으로 교체
- 로드밸런서 : 로드 분산, 두개 회선, 속도 두배

## 라우팅이냐, 스위칭이냐?
- 스위치가 라우터에 비해...
  - 저렴한 가격
  - 빠른 속도
  - 편리한 구성
- 왜 라우터를 써야하죠?
![image](https://github.com/boboram/TIL/assets/14108487/a44a4ffd-4675-40bd-b2b1-8dc8c9e3a8fd)

- 브로드 캐스트 영역을 나누기 위함
- 보안 기능 : 패킷을 필터링함
- 로드 분배
- QoS(Quality of Service) : 트래픽 전송 순서 조정 

# velog
- 링크 : https://velog.io/@bona/cisco-network-v1-part-04
