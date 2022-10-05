# [8.1버전에서 7.4 버전으로 PHP 낮추기](https://velog.io/@bona/PHP-%EB%B2%84%EC%A0%84-%EB%8B%A4%EC%9A%B4%EA%B7%B8%EB%A0%88%EC%9D%B4%EB%93%9C-%EC%9B%90%ED%95%98%EB%8A%94-%EB%B2%84%EC%A0%84-%EC%84%A0%ED%83%9D%ED%95%98%EA%B8%B0)

# nginx 🍯TIP
- EC2 수정시 sudo service nginx restart 처리하기 전에 구성한 부분이 구릿하다 싶으면 아래 명령어를 통해 nginx 구성을 테스트 할 수 있다.
```
sudo nginx -t
```
- restart : `sudo service nginx restart`

# codedeploy-agent 관련 명령어
```
sudo service codedeploy-agent status
sudo service codedeploy-agent start
sudo service codedeploy-agent stop
sudo service codedeploy-agent restart
```
- 로그 확인 : `tail /var/log/aws/codedeploy-agent/codedeploy-agent.log`
