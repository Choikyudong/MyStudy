# if 문

많은 프로그래밍 언어들은 if문을 지원한다.  
저마다 문법은 조금씩 틀리지만 하고자하는 의도는 비슷하다.
> if 문 문법은 각 언어별로 따로 확인바람.

### 일반적인 경우를 처리하는 코드 작성 후 예외 처리를 하자.
```js
if (order != null) {
    if (order.isPayed()) {
        if (order.hasStock()) {
		    // [주 목적] 실제 주문 처리 로직 (가장 깊은 곳에 숨어있음)
		    shipProduct(order);
		} else {
		    showError("재고 없음");
		}
    } else {
		showError("결제 필요");
    }
} else {
    showError("주문 정보 없음");
}
```
위의 코드를 아래와 같이 바꿔보자.
```js
// 1. 예외적인 조건들을 먼저 쳐낸다 (Early Return)
if (order == null) {
  return;
}
if (!order.isPayed()) {
  return;
}
if (!order.hasStock()) {
  return;
}

// 2. [주 목적] 일반적인 정상 흐름이 들여쓰기 없이 깔끔하게 드러남
shipProduct(order);
```
> 개인적으로 많이 사용하는 방법으로 가독성이 좋아진다고 생각함.
> 중첩 if문은 최대한 안쓰려고도 하는편.

### 동치에 대해서 정확하게 이동 경로를 정하라.
```js
let arr = [ ...copyArr ];
for (let i = 0; i < 5; i++) {
  if (i <= 5) {
    arr[i] = cal();
  }
}
```

저자는 배열, 반복분 인덱스와 같이 하나의 차이로 인한 오류가 생각보다 많기에,  
위처럼 `<=` 또는 `>=` 대신 `>`, `<` 확실하게 표현하는 것을 권장한다.
```js
let arr = [ ...copyArr ];
for (let i = 0; i < 5; i++) {
  if (i < 6) {
    arr[i] = cal();
  }
}
```
> 명확하게 표현하자는 의도는 좋지만, 무조건적으로 따를 필요는 없다.

### if문에 의미있는 명령문을 작성.
```js
if (SomeCondition()) {
  // ...
} else {
  doSomething();
}
```
if문을 비우거나 주석만 남기는 경우를 본적이 있는데 의도는 알겠으나,  
최선이였을까?라는 생각은 들었다.

아래와 같이 한 번 변경을 해보자.
```js
// 뭔가가 아닐때!
if (!SomeCondition()) {
  doSomething();
}
```
개인적으로는 if문에서 뭔가를 실행을 하는게 좀 더 맞다고 생각한다.  
추가적으로 `!` 부정형으로 할 경우 `주석`도 함께 써주면 가독성이 조금은 더 올라가지 않을까 싶다.

### 연속적인 경우
```js
if (!inputChar || typeof inputChar !== 'string' || inputChar.length !== 1) {
  return "INVALID_INPUT";
} else if (
    inputChar === '!' ||
    inputChar === '?' ||
    inputChar === '.' ||
    inputChar === ',' ||
    inputChar === ';' ||
    inputChar === ':' ||
    inputChar === '-' ||
    inputChar === '_'
) {
  return "PUNCTUATION";
} else if (
  'a' <= inputChar && inputChar <= 'z' ||
  'A' <= inputChar && inputChar <= 'Z'
) {
  return "IsControl"
} else if (inputChar >= '0' && inputChar <= '9') {
  return "NUMBER";
} 
```
위와 같은 함수를 작성시 아래와 같이 해보자.
1. 복잡한 테스트는 함수 호출로 하자.
2. 가장 흔한 경우를 앞에 두자.
3. 모든 경우를 다루었는지 확인하자.

아래는 위의 규칙을 기반으로 리팩토링하였다.
```js
if (!isValidInput(inputChar)) {
  return "INVALID_INPUT";
}

if (isAlphabet(inputChar)) {
  return "ALPHABET";
} else if (isNumber(inputChar)) {
  return "NUMBER";
} else if (isPunctuation(inputChar)) {
  return "PUNCTUATION";
} else {
  return "UNKNOWN_SYMBOL";
}
```

이렇게 리팩토링을 하면 좋지만 사실 더 좋은 방법은,  
사용하는 언어가 지원된다면 `swich(case)` 문으로 작성하는 것이라고 생각한다.
> 개인적으로는 if문이 `5개 이상`이 되는 경우부터는 switch문으로 작성하는 것을 고려하는 편이다.
> AI로 작성하는 시대이지만 인간다운 소신은 가져보자.