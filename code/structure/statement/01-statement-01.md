# 명령문

## 순서가 중요한 명령문
코드들은 **의존성**을 가지는 경우가 많다.
```java
data = readData();
results = calculateResultsFromData(data);
printResulsts(resulsts);
```
위의 코드를 읽으면
1. 데이터를 읽기
2. 읽어온 데이터를 계산하여 결과를 도출
3. 결과를 출력
순으로 진행된다는게 한눈에 보인다.  
그리고 아래의 코드를 보자.

```java
revenue.ComputeMonthly();
revenue.ComputeQuarterly();
revenue.ComputeAnnual();
```
위의 코드를 보면 분기별 계산이 월별로 하고, 분기별로 하는지  
독립적인지 **호출부**만 보고 판단이 힘들다.

이런 **모호함**은 코드를 읽는 사람이 **구현부**까지 뜯어보게 만든다.  

다음 코드를 살펴보자.
```java
order.validate();
order.applyDiscount();
order.calculateTax();
```
해당 로직은 기능상 아무 문제가 없으며 컴파일 역시 문제없이 된다.  
다만 여기서 모호함은 order가 어떤 순서가 중요한지 의존성이 무엇인지 확인을 위해,  
**구현부**를 다시 확인하는 일이 생길 수 있다.

다음과 같이 해보자.
```java
// 하나의 단일 진입점으로 순서를 명시하기
Class Order {
  void confirm() {
    this.validate();
    this.applyDiscount();
    this.calculateTax();
  }
  // ...
}

// 함수형 스타일로 순서를 명시
Order result = Function
    .<Order>identity()
    .andThen(OrderCalculator::validate)
    .andThen(OrderCalculator::applyDiscount)
    .andThen(OrderCalculator::calculateTax)
    .apply(order);

/*
주석으로 설명하기
*/
order.validate();
order.applyDiscount();
order.calculateTax();
```
위 방법대로 꼭 따라가야할 않아도 된다.

중요한건 각 프로젝트나 팀이나 본인의 스타일에 맞춰서 **모호함**을 최대한 없애주자.
