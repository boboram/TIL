# troubleshooting
- 문제 해결

## [s3 파일 업로드시 SignatureDoesNotMatch 문제 해결](https://velog.io/@bona/troubleshooting-asw-SignatureDoesNotMatch)

## [PHPStorm | phpunit 모든 테스트 확인](https://velog.io/@bona/PHPStorm-phpunit-%EB%AA%A8%EB%93%A0-%ED%85%8C%EC%8A%A4%ED%8A%B8-%ED%99%95%EC%9D%B8)

## [macOs Monterey 업그레이드 후 git 오류 해결](https://velog.io/@bona/macOs-Monterey-%EC%97%85%EA%B7%B8%EB%A0%88%EC%9D%B4%EB%93%9C-%ED%9B%84-git-%EC%98%A4%EB%A5%98-%ED%95%B4%EA%B2%B0)

## 브랜치 생성안하고 master로 바로 push 한 경우 해결
- 과정
  - 최근 커밋 내역 취소 : `git reset HEAD^`
  - master 브랜치에 푸시 못하도록 처리 
    - 프로젝트 > Settings > Repository > Protected branches > Allowed to push - `No one` 옵션 선택
    - 으로 하면 push를 막을 수 있다. 
