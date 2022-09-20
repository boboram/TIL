# [php artisan optimize:clear 오류 해결](https://velog.io/@bona/Laravel-php-artisan-cache-permission-%ED%95%B4%EA%B2%B0)

# ORM 참조 로딩 방식  
## LAZY 로딩? EAGER 로딩?
- EAGER(즉시로딩) : 언제나 **한 번의 쿼리**로 모든 정보를 가져온다. 
  - 참조 객체와 항상 함께 로드되어야 하는 조건을 가진 엔티티라면 LAZY 방식보다는 EAGER 방식이 더 좋음 
  - `N+1`을 해결할 수 있음 
- LAZY(지연로딩) : 필요시에만 관계된 쿼리를 조회한다. 
  - 참조가 많다면, 프로젝트가 크다면, 해당 참조를 항상 사용하지 않아도 되는 경우라면! LAZY 로딩을 사용하는 것이 좋다. 

### N+1 문제란? 
- 연관 관계에서 발생하는 이슈로 연관 관계가 설정된 데이터를 조회할 경우에 조회된 데이터 갯수(n) 만큼 연관관계의 조회 쿼리가 추가로 발생하여 데이터를 읽어오게 된다.
- 조회 데이터가 10개라면 연관관계의 조회 쿼리가 10번 호출되고 10만개라면 10만개...ㄸㄹㄹ
- N 수가 크면 클수록 성능에 큰 문제가 발생할 수 있다.


## 라라벨 로딩 방식
- load : EAGER 방식 사용
- with : LAZY 방식 사용
- loadMissing : 처음에 로딩하지 않은 경우에만 EAGER, 그 후엔 LAZY 

## 정리
- 데이터가 많으면서 해당 데이터들의 연관관계가 항상 쓰이지 않는 프로젝트라면 LAZY 로딩 사용을 권장하고 있다. 

# 라라벨 프로젝트 생성 후 권한 설정
composer create-project laravel/laravel 프로젝트명 —prefer-dist

mkdir -p ./storage/framework/{sessions,views,cache}
mkdir -p ./storage/logs
mkdir -p ./bootstrap/cache

cd storage/
mkdir -p framework/{sessions,views,cache}
chmod -R 775 framework
