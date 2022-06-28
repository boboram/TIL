# 8.1버전에서 7.4 버전으로 PHP 낮추기
- 상황 : 원래는 PHP 7.4였는데 8.1로 변경된 상황에서 다운그레이드 해야 하는 상황이여서 PHP 버전만 바꿔주면 되는 경우였다.

- 순서 
  - 기존 사용중인 ec2로 새로운 ec2 복사본 생성
  - 해당 ec2 접속 
  - 아래 명령어 실행
```
sudo update-alternatives --config php
```
<img width="809" alt="image" src="https://user-images.githubusercontent.com/14108487/176100292-401dc5ef-8fa9-45fa-99b5-d45d93c71b84.png">
- 이미지에서 변경하고자 하는 버전의 번호(Selectiong)를 선택하면 된다. 7.4가 1이였기 때문에 1 입력후 엔터 
<img width="815" alt="image" src="https://user-images.githubusercontent.com/14108487/176100593-95c6dd4a-db51-42f0-9aa4-71106ad5c4ca.png">

 - 버전을 확인해보면 7.4로 변했다. : ) 
```
php -v 
```
<img width="634" alt="image" src="https://user-images.githubusercontent.com/14108487/176100675-6d1db938-7706-464e-8570-2246ba6830e9.png">

회사에서는 aws ec2, cdg 기반으로 배포를 하고 있기 때문에 해당 ec2 복사본을 기반으로 ami 생성 -> lc 생성 -> asg에 새로 생성한 lc로 교체하여 기존 코드로 재배포 해줬다.

## update-alternatives 이란?
- 해당 언어에 대해서 여러가지 버전이 존재하는 경우, 원하는 버전으로 실행하고자 할 때 사용 가능
- 사용 방법은 위에 참고하기 
