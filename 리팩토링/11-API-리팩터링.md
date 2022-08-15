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

## 객체 통째로 넘기기 427 ~ 432 page
```
const low = aRoom.daysTempRange.low;
const high = aRoom.daysTempRange.high;
if (aPlan.withinRange(low, high))
```

```
if (aPlan.withinRange(aRoom.daysTempRange))
```
- 다른 객체의 메서드를 호출하면서 호출하는 객체 자신이 가지고 있는 데이터 여러 개는 건데는 경우 

## 매개변수를 질의 함수로 바꾸기 433 ~ 436 page
```
availableVacation(anEmployee, anEmployee.grade);

function availableVacation(anEmployee, grade) {
  //연휴 계산...
```
를
```
availableVacation(anEmployee)

function availableVacation(anEmployee) {
  const grade = anEmployee.grade;
  //연휴 계산...
```
로 바꾸기 

- 매개변수 목록은 함수의 변동 요인을 모아놓은 곳이다. 
- 피호출 함수가 **스스로 쉽게 결정할 수 있는 값을 매개변수로 건네는 것도 일종의 중복**이다. 
  - 질의함수로 대체한 후 매개변수를 제거한다. 
- 대상 함수가 참조 투명해야 한다. (참조 투명 : 함수에 똑같은 값을 건네 호출하면 항상 똑같이 동작한다.) 

## 질의 함수를 매개변수로 바꾸기 437 ~ 441 page
```
targetTemperature(aPlan)

function targetTemperature(aPlan) {
  currentTemperature = thermostat.currentTemperature;
  //생략
```

```
targetTemperature(aPlan, thermostat.currentTemperature)

function targetTemperature(aPlan, currentTemperature) {
  //생략
```
- 전역 변수를 참조한다거나 같은 모듈에 안에서라도 제거하길 원하는 원소를 참조하는 경우라면 해당 참조를 매개변수로 바꿔 해결 할 수 있다. 
- 참조 투명하지 않은 원소에 접근하는 모든 함수는 참조 투명성을 잃게 되는데, 이 문제는 해당 원소를 매개변수로 바꾸면 해결된다. 
