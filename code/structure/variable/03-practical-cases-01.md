# 변수명 지어보기

## 반복문
반복문은 컴퓨터 프로그래밍에서 일반적인 기능이며,  
그렇기에 가이드라인도 존재한다.  
일반적으로 우리는 `i, j, k`와 같은 이름을 관습적으로 사용한다.
```js
// 비즈니스 로직에서도 흔히 보이긴 함.
for (let i = 0; i < userDeleteList.length; i++) {
  userDeleteList[i].status = 0;
}

// 알고리즘 작성할 때 이렇게 많이 했었음.
for (let i = 0; i < 10; i++) {
  for (let j = 0; j < 10; j++) {
    for (let k = 0; k < 10; k++) {
      if (i % 2 != 0) {
        data[j][k] = 1;
      }
    }
  }
}
```
이렇게 **내부**에서만 사용이 된다면 위와같이 작성하여도 큰 문제는 없을 것이다.

그렇기에 내부에서 사용하더라도 `i, j, k`와 같은 네이밍 보다는 의미가 있는 이름으로 작성하는데 조금 더 좋다고 생각한다.
```js
// 좌표로 뭔가를 하는구나를 알 수 있다.
for (let layer = 0; layer < 10; layer++) {
  for (let col = 0; col < 10; col++) {
    for (let row = 0; row < 10; row++) {
      if (layer % 2 != 0) {
        data[col][row] = 1;
      }
    }
  }
}
```
> 다만 이중 반복문에서 저렇게 작성을 이어갈 경우 뭐가 뭔지 스스로 헷갈려질때가 많았다.

다만 변수를 외부에서도 사용해야 한다면 이야기가 완전 달라진다.
```js
let i = 0;
while (isContinue()) {
  score[i] = getNextScore(i);
  i++;
}

if (isCollectPoisition(i)) {
  throw new Error();
}

// i를 사용
```
위의 코드에서 `while`에서는 `i`가 대략적으로 점수를 가져오고 배열의 위치를 파악하기 위한 용도를 추측할 수 있다.  

다만 `i`를 계속해서 사용하는 로직이라면 `i`가 무엇이였는지 코드를 읽고 있는 개발자의 기억력에 의존해야 한다.
> 개인적으로는 사람의 기억력에 의존하는 시스템은 위험하다고 생각한다.

```js
let recordCount = 0;
while (isContinue()) {
  score[recordCount] = getNextScore(recordCount);
  recordCount++;
}

if (isCorrectPosition(recordCount)) {
  throw new Error();
}
```
`recordCount`와 같이 조금 더 명확히 변경해보자.
> 결국 변수명은 해당 로직인지 비즈니스가 무엇인지를 이해하는게 우선이다. `도메인`을 잘 파악을 해야하는게 이런 이유 때문인다.