# composer

## 작업한 컴포저 정식으로 올리기 전에 작업한 브랜치로만 로컬에서 확인해보기 

- 레지스트리 올리기 전에 작업한 컴포저를 로컬에서 확인하려고 한다면!! 
  - 작업 레파지토리를 깃에 푸시하여 푸시한 브랜치로 확인을 할때 canonical:false 옵션을 사용하면 가능하다.  

터미널에 입력 
```
composer config repositories.레파지토리명 '{"type": "vcs","url": "레파지토리경로/","canonical": false,"branches-path": "브랜치명"}'
composer require 컴포저명칭:dev-브랜치명
```

- 레파지토리경로에 `/` 붙일 것 
- require 시에 브랜치명 옆에 `dev-` 붙일 것 
