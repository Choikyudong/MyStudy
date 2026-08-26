# 명령문

## 순서가 중요하지 않은 명령문
순서가 중요하지 않은 경우도 많은데 아래 코드를 먼저보자.
```java
MarketingData marketingData;
SalesData salesData;
TravelData travelData;

travelData.computeQuarterly();
salesData.computeQuarterly();
marketingData.computeQuarterly();

salesData.computeAnnual();
marketingData.computeAnnual();
travelData.computeAnnual();

marketingData.print();
salesData.print();
travelData.print();
```
각 변수들은 의존성이 전혀 없는 독립적인 데이터들이다.  
여기서 `travelData`를 추적하고 싶다면 이리저리 봐야해 어려움을 겪을 수 있다.

기본적으로 코드를 작성시 **하향식**으로 읽을 수 있게 개발해보자.
```java
MarketingData marketingData;
marketingData.computeQuarterly();
marketingData.computeAnnual();
marketingData.print();

SalesData salesData;
salesData.computeQuarterly();
salesData.computeAnnual();
salesData.print();

TravelData travelData;
travelData.computeQuarterly();
travelData.computeAnnual();
travelData.print();
```
다음과 같이 구조를 변경하면 기존에 파편처럼 흩어져있던 그룹들이
**지역화**되어 코드를 읽을 때 범위가 좁아지며 어떤 순서대로 데이터를 처리하는지도 알 수 있게 된다.
> 예전에 참여했던 프로젝트 중 분기별 반기별 년도별 계산을 하는 기능이 있는 프로그램이였는데,  
기능이 파편화가 되어있다보니 고객사PM도 기존 기능을 분석하면서 애를 많이 먹었다는 이야기를 들었던게 생각이 남.