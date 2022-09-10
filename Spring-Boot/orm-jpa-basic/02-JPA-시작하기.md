# 02. JPA 시작하기 

<img width="210" alt="image" src="https://user-images.githubusercontent.com/14108487/189468086-ca083258-7b9e-4f60-80a7-f9f242667077.png">
- /Users/bona/test 로 지정하여 h2 데이터베이스 생성

## JPA CRUD
- 실무에서는 스프링을 사용하기 때문에 em.persist만 작성하면 끝! 
## insert
```
EntityManager em = emf.createEntityManager();

EntityTransaction tx = em.getTransaction();
tx.begin();

try {
    Member member = new Member();
    member.setId(1L);
    member.setName("HelloA");
    em.persist(member);

    tx.commit();
} catch (Exception e) {
    tx.begin();
} finally {
    em.close();
}
```
## select
```
Member findMember = em.find(Member.class, 1L);
System.out.println("findMember.id = " + findMember.getId()); //1
System.out.println("findMember.name = " + findMember.getName()); //HelloA
```

## delete
```
EntityManager em = emf.createEntityManager();

EntityTransaction tx = em.getTransaction();
tx.begin();

try {
     Member removeMember = em.find(Member.class, 1L);
    em.remove(removeMember);

    tx.commit();
} catch (Exception e) {
    tx.begin();
} finally {
    em.close();
}
```

## update
```
EntityManager em = emf.createEntityManager();

EntityTransaction tx = em.getTransaction();
tx.begin();

try {
  Member member = em.find(Member.class, 2L);
  member.setName("boram"); 
    tx.commit();
} catch (Exception e) {
    tx.begin();
} finally {
    em.close();
}
```
- update는 신기하게 persist 가 아니라 `member.setName("boram");`만 작성해도 update 가 실행된다고 한다. 
## 주의
- 엔티티 매니저 팩토리는 **하나만 생성**해서 애플리케이션 전체에 서 공유
- 엔티티 매니저는 쓰레드간에 공유X (사용하고 버려야 한다). 
- JPA의 모든 데이터 변경은 **트랜잭션 안**에서 실행


## JPQL
- JPA를 사용하면 검색시에도 엔티티 객체를 대상으로 검색하기 때문에 JPQL을 이용하여 원하는 검색 쿼리 작성 가능  
- 엔티티 객체를 대상으로 쿼리를 실행하기 때문에 DB 종류에 상관없이 쿼리 작성 가능 
```
List<Member> result = em.createQuery("select m from Member as m", Member.class)
//                  .setFirstResult(5) //limit -> DB 종류에 따라서 쿼리문이 변경됨
//                  .setMaxResults(10) //offset -> DB 종류에 따라서 쿼리문이 변경됨
                    .getResultList();

for (Member member : result) {
    System.out.println("member.name = " + member.getName());
}
```
### 실제 쿼리
```
select
        m 
from
    Member as m */ select
        member0_.id as id1_0_,
        member0_.name as name2_0_ 
    from
        Member member0_
```
- select m 만 했음에도 컬럼 2개가 select 됨! 
