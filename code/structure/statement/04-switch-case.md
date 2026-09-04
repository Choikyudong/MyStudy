# switch 문

현세대에 많은 언어들은 `switch`를 지원한다.  
다만 언어들마다 문법은 조금씩 다 다르다.

또한 `switch`는 시대에 따라 조금씩 문법이 진화해왔다.

### switch 문법의 최신화.
자바를 예시로 보면 다음과 같다.
```java
// 전통적인 switch문
input = command[0];
switch (input) {
	case "A":
        // ...
        break;
    case "B":
        // ... 
        break;
    case "C":
        // ... 
        break;
}
```
단일 조건문으로 매칭시 실행이 되는 것이 많이들 배운 `switch`였고 다중 조건이 필요할 시 아래와 같이 하였다.
```java
input = command[0];
if (input.equals("A") || input.equals("Z")) {
    // ...
} else if (input.equals("B")) {
    // ...
}
```

현재는 많은 언어들이 진화를 하였다.
```java
input = command[0];
switch (input) {
    case "A", "Z"  -> // ... (A 또는 Z일 때 실행)
    case "B"       -> // ...
    case "C"       -> // ...
}
```
현재의 많은 언어들은 `break`를 생략하여도 되도록 변경하고 있으나,  
`break`를 써야하는 문법이라면 꼭 `break`를 써서 `fall-through`을 막자.

> 이처럼 기본 문법이라고 배운 `switch`는 버전별로 변화를 가진 언어도 있다.

### default 문
때로는 `case`문에 기본 에러 처리를 하는 경우가 있는데,  
if문의 `else`처럼 `default`로 검출을 하도록 하자.

```java
input = command[0];
switch (input){
    case "A", "Z" -> // ...
    case "B" -> // ...
    case "C" -> // ...
    case "D" -> {
        // 이렇게 case를 억지로 늘려서 에러 처리하지 말 것
        return ...
    }
}
```
기본 에러 처리를 위해 억지로 `case`를 만들지 말고, 아래와 같이 수정을 해보자.

```java
input = command[0];
switch (input){
    case "A", "Z" -> // ...
    case "B" -> // ...
    case "C" -> // ...
    default -> // 기본 오류임..
}
```
주석과 `case`로 억지로 매듭을 짓지말고, 각 case는 의미있게 사용하고    
기본적인 처리들은 `default`를 써서 최대한 의미가 있게 사용하자.

> 언어마다 문법 차이가 있으니 참고바람.
