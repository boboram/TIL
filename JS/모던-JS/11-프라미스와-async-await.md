# 11. 프라미스와 async, await

## 콜백

- 동기 : A가 실행이 끝나야만 B가 실행될 수 있다. 
```
let promise = new Promise(function(resolve, reject) {
  // executor (제작 코드, '가수')
});
```
- `resolve` : 성공시 결과 콜백 
- `reject` : 실패시 결과 콜백 
- 상태
  - resolve, reject 인 상태 : settled(처리된)
  - 실행중인 경우 : pending(대기)
- finally
```
new Promise((resolve, reject) => {
  setTimeout(() => resolve("결과"), 2000)
})
  .finally(() => alert("프라미스가 준비되었습니다.")) //프라미스가 준비되었습니다.
  .then(result => alert(result)); // <-- .then에서 result를 다룰 수 있음 //결과 
  .catch(err => alert(err)); // <-- .catch에서 에러 객체를 다룰 수 있음
```
- finally 실행 후 결과 전달
- 성공시 finally -> then 
- 실패시 : finally -> catch

## promise chaining
### fetch
- fetch : 프론트 단에서 url 요청시 많이 사용 
```
fetch('/article/promise-chaining/user.json')
  .then(response => response.json()) //response를 json 형태로 불러오기 
  .then(user => alert(user.name)); // Violet-Bora-Lee, 이름만 성공적으로 가져옴
```
- async ~ await 
