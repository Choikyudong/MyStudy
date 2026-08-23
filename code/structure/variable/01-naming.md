# 변수명

변수는 귀엽게, 보기 좋게 하기 위해 작성하지 않는다.

나쁜 변수명의 예시이다.
```
x = 5;
abc = calTax(aaa);

zzz = x + abc % 100;
```
여기에서 사용된 변수명들은 도대체 뭘 의미하는지 알기 어렵다.

많은 개발자들은 위와 같은 변수명들을 아래와 같이 작성하려고 한다.
```
incentive = 5.0;
taxAmount = calculateTax(monthlySalary);

PERCENTAGE_BASE = 100.0;
netPay = baseSalary - taxAmount + (incentive / PERCENTAGE_BASE);
```
위와같이 각 변수가 **완전**하고 **정확**히 설명하는지가 가장 중요하다.

이름은 가능한 구체적으로 작성하는게 좋다.  
개인적으로 오늘 날짜에 대한 변수명을 짓는다면  
```
c, cd, date, current
```
와 같은 변수명 보다는
```
currentDate, nowDate, todayDate
```
와 같은 형식을 조금 더 선호한다.

우리는 때로
```
x, temp, y, i, array, list
```
등 한 가지 이상의 목적을 가질 수 있는 이름을 많이 사용하는데, 이런 쉽고 막연한 이름들은 정보 제공도 원할히 되지않아 나쁜 이름에 가깝다.

> 나도 때로는 `userList` 이렇게 작성을 한적이 꽤 있는데 돌이켜 생각해보면, 이게 어떤 사용자 목록인지 **명확**히 알기가 어려웠다.
