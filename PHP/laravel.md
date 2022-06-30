# php artisan optimize:clear 오류 해결

명령어를 입력하는데 오류가 발생했다. 

<img width="523" alt="image" src="https://user-images.githubusercontent.com/14108487/176361437-b911efd5-9e07-45f7-99d1-2e51f2efd658.png">

인터넷에 찾아보니 cache/data 폴더가 없어서 그런거라고 한다.

아래 명령어를 사용하여 폴더 생성및 권한을 추가했고 다시 optimize:clear 명령어를 쳐보니 문제없이 동작된다. : ) 

```
sudo mkdir -p /프로젝트경로/storage/framework/cache/data
sudo chown -R 사용자:www-data /프로젝트경로/storage/framework/cache/data
```

## 사용자:www-data로 권한을 준 이유는?
www-data로 해야만 웹서버에 대한 데이터를 받을 수 있다. 그렇지 않다면 500에러를 경험할 수 있다. : ) 
