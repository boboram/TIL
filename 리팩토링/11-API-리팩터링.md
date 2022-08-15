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

## 함수 매개변수화하기 417 ~ 420 page
```
function tenPercentRaise(aPerson) {
  aPerson.salary = aPerson.salary.multiply(1.1);
}

function fivePercentRaise(aPerson) {
  aPerson.salary = aPerson.salary.multiply(1.05);
}
```

```
function raise(aPerson, factor) {
  aPerson.salary = aPerson.salary.multiply(1 + factor);
}
```
- 두 함수의 로직이 아주 비슷하고 단지 리터럴 값만 다르다면, 그 다른 값만 매개변수로 받아 처리하는 함수 하나로 합쳐서 중복을 없앨 수 있다. 


## 플래그 인수 제거하기 421 ~ 426 page
```
function setDimension(name, value) {
  if (name === "height") {
    this._height = value;
    return;
  }
  if (name === "width") {
    this._width = value;
    return;
  }
}
```

```
function setHeight(value) {this._height = value;}
function setWidth (value) {this._width = value;}
```
- 플래그 인수란 호출되는 함수가 실행할 로직을 호출하는 쪽에서 선택하기 위해 전달하는 인수 
- 호출할 수 있는 함수들이 무엇이고 어떻게 호출해야 하는지를 이해하기가 어려워ㅓ진다. 
- 절차
  - 매개변수로 주어질 수 있는 값 각각에 대응하는 명시적 함수들을 생성한다.
  - 원래 함수를 호출하는 코드들을 모두 찾아서 각 리터럴 값에 대응되는 명시적 함수를 호출하도록 수정한다. 
