# 변수명 지어보기

## 상태 변수
컴퓨터 공학에서 `상태(state)`란 시스템 또는 프로그램이 특정 시점에 가지고 있는 조건을 말한다.

보통 상태 변수를 쓸 때 `flag`라는 이름을 많이 쓴다.
```rust
if flag {
  // ...
}

let status_flag: u8 = 0x80;
if (status_flag & 0x0F) != 0 {
  // ...
}
```
여기서 `flag`가 무슨 상태를 누구, 어떤 것을 의미하는지 파악하기 어려우며 `status_flag` 같은 경우는 문서나 설명을 듣기전까지 파악하기 어려울 수 있다.
> 주석까지 없으면 눈물 나지 않을까 싶다.

```rust
// 하위 4비트는 에러 상태를 의미함.
const ERROR_MASK: u8 = 0x0F;

let status_flag: u8 = 0x80;

let has_error = (status_flag & ERROR_MASK) != 0;
if has_error {
  // ...
}
```
코드를 볼 때 **이해**해야 하는 부분이 있다면 변수의 이름을 다시 만드는 걸 고려해보자.

코드를 추리하고 범인을 찾는거도 재미일 수 있지만 코드는 추리의 대상이 아니다. 
>코드는 직관적으로 바로 이해할 수 있는게 가장 좋다고 생각한다.

## 불린 변수명
개인적으로는 `is`를 붙이는걸 선호한다.
```rust
// 단순 존재/상태 여부
let is_ready: bool = true;

// 소유/포함 여부
let has_token: bool = true;

// 가능 여부
let can_execute: bool = true;
```
다만 저자는 `is`를 붙이면 의문사가 되어 모호한 답이 되어 아래와 같이 제안을 한다.
```rust
let ready: bool = true;
let token: bool = true;
let execute: bool = true;
```
어떤 스타일을 채택하던 각 팀의 방향에 맞춰 작성하자.
> 대부분의 언어/프레임워크(Java, Js 등)에서는 `is`, `has`를 붙여 쓰는 스타일을 조금 더 많이 보이기는 한다.

## 추천하지 않는 유형들
is, has 등을 붙이지 않는것은 상관이 없으나 아래와 같은 스타일은 지양하는것이 좋다.
```rust
let is_not_ready: bool = true;
let has_not_token: bool = true;
let can_not_execute: bool = true;
```
위와 같이 부정형을 붙이면 해당 변수가 **부정형**이 되었을 때 읽기가 힘들어져 되도록이면 사용하지 않은것을 추천한다.
```rust
// 준비가 안되었다면
if !is_ready {
  // ...
}

// 준비 안된게 아니라면??
if !is_not_ready {
  // ...
}
```
bool 타입 변수명 작성시 아래 내용을 고려해보자.
1. 부정형 접수자 금지 (기존 변수에 `!`연산자를 이용하자)
2. 부정적 의미 단어 대신 긍정형 사용 (disabled -> enabled)