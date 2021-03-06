# JUnit 들여다보기 

## JUnit 프레임워크 
> 아틀란타 행 비행기를 타고 가나 JUnit을 만들었다. 비좁은 기내에서 엔지니어 둘이 랩탑을 꺼내 코드를 짜는 일 밖에 다른 무엇을 하겠는가?

멋있다..❤️

JUnit은 이미 훌륭한 모듈이지만 우리는 보이스카우트 원칙을 따뤄야 한다.
- 보이스카우트 규칙은 처음 왔을 때보다 자리를 더 깨끗하게 해야 하는 것. 즉 코드도 내가 처음 봤을 때보다 더 깨끗하게 만들어야 한다는 규칙
- 해당 장에서는 JUnit을 리팩토링하는 과정을 보여준다.

그 중에서도 
## 기억 나는 것들 
- 현시대에 사용하지 않는 프리픽스는 제거하자. 
- 함수로 뺄 수 있는 식들은 올바른 이름의 함수로 뺀다. 
- 숨겨진 시간적인 결합: A 실행 후 B를 실행해야만 올바른 결과가 도출되는 것 
  - 정처기에서 그랬다.. 결합은 낮고 응집은 높아야 한다고..
  - 이런 경우라면 한 함수에 해당 과정을 넣어줘야 한다. 
- 논리적으로 의문이 드는 식이 있다면 고쳐라. 테스트를 하면서 고쳐라. 
- 분석함수가 나오고서 조합 함수가 그 뒤를 이어서 나오는 것이 깔끔 
- 코드를 리팩터링 하다보면 원래 했던 변경을 되돌리는 경우도 다반사, **리팩터링은 코드가 어느 수준에 이를 때까지 수많은 시행착오를 반복하는 작업이기 때문** 

## 느낀점
아무리 좋은 코드라도 개선이 불필요한 모듈은 없다는 저자의 말이 와닿았다. 하지만 무식하게 리팩터링을 시작하면 처음보다 더 안좋아질 수 있다는 것도 명심해야겠다.
