## 배경
- 객체답게 모델링 할수록 매핑 작업만 늘어난다...
- 객체를 자바 컬렉션에 저장 하듯이 DB에 저장할 수는 없을까?
- JPA 탄생 : Java Persistence API
  - Persistence : 영속성 

## JPA?
- 자바 진영의 ORM 표준
- 쿼리를 개발자가 안만들고 JPA가 만들어줌 
- **패러다임의 불일치 해결**

## ORM? 
- Object-relational mapping(객체 관계 매핑) 
- 객체와 DB를 ORM이 중간에서 매핑
- 대중적인 언어에는 대부분 ORM 기술이 존재 
- ORM은 객체와 RDB 두 기둥위에 있는 기술 
  - 객체와 RDB 두개 모두 잘 알고 있어야 함

### 신뢰할 수 있는 엔티티, 계층
- JPA를 사용하면 `member.getOrder().getDeliver();` 형식의 영속적인 조회가 가능
  - 동일한 트랜잭션에서 조회한 엔티티는 같음을 보장(`jpa.find(Member.class, memberId);`)
  - 같은 트랜잭션 안에서는 같은 엔티티를 반환 - 약간의 조회 성능 향상
- 기존 자바에서 DAO를 사용한다면 필요한 것을 따로따로 조회했어야 함 
