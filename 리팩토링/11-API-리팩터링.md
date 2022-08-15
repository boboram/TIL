# 11. API 리팩터링

## 질의 함수와 변경 함수 분리하기 413 ~ 416 page
```
function getTotalOutstandingAndSendBill() {
  const result = customer.invoices.reduce((total, each) => each.amount + total, 0);
  sendBill();
  return result;
}
```

```
function totalOutstanding() {
  return customer.invoices.reduce((total, each) => each.amount + total, 0);
}

function sendBill() {
  emailGateway.send(formatBill(customer));
}
```

- 외부에서 관찰할 수 있는 겉보기 부수효과가 전혀 없이 값을 반환해주는 함수를 추구해야 한다.   
  - 이용할 때 신경 쓸 거리가 매우 적다. 
- 질의 함수(읽기 함수)는 모두 부수효과가 없어야 한다. 

## 함수 매개변수화하기 
