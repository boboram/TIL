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
- 전역 변수를 참조한다거나 같은 모듈 안에서라도 제거하길 원하는 원소를 참조하는 경우라면 해당 참조를 매개변수로 바꿔 해결 할 수 있다. 
- 참조 투명하지 않은 원소에 접근하는 모든 함수는 참조 투명성을 잃게 되는데, 이 문제는 해당 원소를 매개변수로 바꾸면 해결된다. 

## 세터 제거하기 442 ~ 444 page
```
class Person {
  get name() {...}
  set name(aString) {...}
```

```
class Person {
  get name() {...}

```

- 세터 메서드는 필드가 수정될 수 있다는 뜻이다. 
- 객체 생성 후에는 수정되지 않길 원하는 필드라면 세터를 제공하지 않았을 것이다. 
- 세터 제거하기가 필요한 상황
  - 사람들이 무조건 접근자 메서드를 통해서만 필드를 다루려 하는 경우 
  - 클라이언트에서 생성 스크립트를 사용해 객체를 생성하는 경우

## 생성자를 팩터리 함수로 바꾸기 445 ~ 447 page
```
leadEngineer = new Employee(document.loadEngineer, 'E');
```

```
leadEngineer = createEngineer(document.leadEngineer);

function createEngineer(name) {
  return new Employee(name, 'E');
}
```

- 생성자 제약 : 자바 생성자는 반드시 그 생성자를 정의한 클래스의 인스턴스를 반환해야 한다. 생성자의 이름도 고정되어, 기본 이름보다 더 적절한 이름이 있어도 사용할 수 없다.
- 팩터리 함수에는 이러한 제약이 없다. 

## 함수를 명령으로 바꾸기 448 ~ 455 page
```
function score(candidate, medicalExam, scoringGuide) {
  let result = 0;
  let healthLevel = 0;
  //긴 코드 생략
}
```

```
class Scorer {
  constructor(candidate, medicalExam, scoringGuide) {
    this._candidate = candidate;
    this._medicalExam = medicalExam;
    this._scoringGuide = scoringGuide;
  }
  
  execute() {
    this._result = 0;
    this._healthLevel = 0;
    //긴 코드 생략
  }
}
```

- 함수를 그 함수만을 위한 객체 안으로 캡슐화하면 더 유용해지는 상황이 있다. -> **명령 객체**
  - 메서드 하나로 구성되며, 이 메서드를 요청해 실행하는 것이 이 객체의 목적이다. 
  - 복잡한 함수를 잘게 쪼개서 이해하거나 수정하기 쉽게 만들고자 할 때 

## 명령을 함수로 바꾸기 456 ~ 460
```
class ChargeCalculator {
  constructor(customer, usage) {
    this._customer = customer;
    this._usage = usage;
  }
  
  execute() {
    return this._customer.rate * this._usage;
  }
}
```

```
function charge(customer, usage) {
  return customer.rate * usage;
}
```
- 명령 객체는 복잡한 연산을 다룰 수 있는 강력한 매커니즘을 제공한다. 
- 로직이 크게 복잡하지 않다면 명령 객체는 장점보다 단점이 크니 평범한 함수로 바꿔주는 게 낫다.  

## 수정된 값 반환하기 461 ~ 464 page 
```
let toalAscent = 0;
calculateAscent();

function calculateAscent() {
  for (let i = 1; i < points.length; i++) {
    const verticalChange = points[i].elevation - points[i-1].elevation;
    totalAscent += (verticalChange > 0) ? verticalChange : 0;
  }
}
```

```
const totalAscent = calculateAscent();

function calculateAscent() {
  let result = 0;
  for (let i = 1; i < points.length; i++) {
    const verticalChange = points[i].elevation - points[i-1].elevation;
    result += (verticalChange > 0) ? verticalChange : 0;
  }
  
  return result;
}
```
- 데이터가 어떻게 수정되는지를 추적하는 일은 코드에서 이해하기 가장 어려운 부분 중 하나다. 
- 데이터가 수정된다면 그 사실을 명확히 알려주어서, 어느 함수가 무슨 일을 하는지 쉽게 알 수 있게 하는 일이 대단히 중요하다.
- 수정된 값을 반환하여 호출자가 그 값을 변수에 담아두도록 하는 것이 데이터가 수정됨을 알려주는 좋은 방법이다. 
  - 호출자 코드를 읽을 때 변수가 갱신될 것임을 분명히 인지하게 된다. 
- 값 하나를 계산한다는 분명한 목적이 있는 함수들에 가장 효과적이고, 반대로 값 여러 개를 갱신하는 함수에는 효과적이지 않다. 
 
## 오류 코드를 예외로 바꾸기 465 ~ 470 page 
```
if (data)
  return new ShippingRules(data);
else
  return -23;
```

```
if (data)
  return new ShippingRules(data);
else
  return new OrderProcessingError(-23);
```

- 예외를 사용하면 오류코드를 일일이 검사하거나 오류를 식별해 콜스택 위로 던지는 일을 **신경 쓰지 않아도 된다**. 
- 정상 동작 범주에 들지 않는 오류를 나타낼 때만 쓰여야 한다. 
 
## 예외를 사전확인으로 바꾸기 471 ~ 474 page 
```
double getValueForPeriod (int periodNumber) {
  try {
    return values[periodNumber];
  } catch (ArrayIndexOutOfBoundsException e) {
    return 0;
  }
}
```

```
double getValueForPeriod (int periodNumber) {
  return periodNumber >= values.length) ? 0 : values[periodNumber];
}
```
- 함수 수행 시 문제가 될 수 있는 조건을 함수 호출 전에 검사할 수 있다면, 예외를 던지는 대신 호출하는 곳에서 조건을 검사하도록 해야 한다.  
