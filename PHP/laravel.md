# [php artisan optimize:clear 오류 해결](https://velog.io/@bona/Laravel-php-artisan-cache-permission-%ED%95%B4%EA%B2%B0)

# ORM 참조 로딩 방식  
## LAZY 로딩? EAGER 로딩?
- EAGER(즉시로딩) : 언제나 한 번의 쿼리로 모든 정보를 가져온다. 
  - 참조 객체와 항상 함께 로드되어야 하는 조건을 가진 엔티티라면 LAZY 방식보다는 EAGER 방식이 더 좋음 
  - `N+1`을 해결할 수 있음 
- LAZY(지연로딩) : 필요시에만 관계된 쿼리를 조회한다. 
  - 참조가 많다면, 프로젝트가 크다면, 해당 참조를 항상 사용하지 않아도 되는 경우라면! LAZY 로딩을 사용하는 것이 좋다. 

## 라라벨 로딩 방식
- load : EAGER 방식 사용
- with : LAZY 방식 사용
- loadMissing : 처음에 로딩하지 않은 경우에만 EAGER, 그 후엔 LAZY 

## 정리
- 데이터가 많은 프로젝트에서는 LAZY 로딩 사용을 권장하고 있다. 
