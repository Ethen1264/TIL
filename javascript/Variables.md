# Variables

### Var

#### Scope of var

Scope는 변수를 사용할 위치를 의미한다. `var`는 `전역 범위` `함수 범위`로 나누어진다.

`var`가 함수외부에서 선언될 시 전역 Scope이다.
`var`가 함수안에서 선언될 시 함수 Scope이다.

```tsx
var greeter = "hey hi";

function newFunction() {
  var hello = "hello";
}
```

여기서 greeter는 전역 범위 hello는 함수 범위이다.

```tsx
var tester = "hey hi";

function newFunction() {
  var hello = "hello";
}
console.log(hello); // error: hello is not defined
```

이것처럼 hello는 함수범위이기 때문에 전역에서 호출하면 에러가 나타난다.

#### var 변수는 재선언되고, 업데이트될 수 있다.

같은 범위 내에서라면 아래의 두 경우와 같이 수정이 가능하며 에러가 발생하지 않는다.

```tsx
var greeter = "hey hi";
var greeter = "say Hello instead";
```

```tsx
var greeter = "hey hi";
greeter = "say Hello instead";
```

#### var의 호이스팅

호이스팅이란 변수와 함수 선언이 맨 위로 이동되는 것 이다.

```tsx
console.log(greeter); // undefined
var greeter = "say hello";
```

#### var의 문제점

```tsx
var greeter = "hey hi";
var times = 4;

if (times > 3) {
  var greeter = "say Hello instead";
}

console.log(greeter); // "say Hello instead"
```

위와 같이 우선적으로 전역에서 greeter를 선언 + 초기화 한다. 그후 조건문안에서 greeter를 새롭게 선언 + 초기화한다. 이렇게 한 후 다시 전역에서 greeter를 호출하면 애러가 발생하지 않고 함수 안에서 선언했던 greeter가 출력된다. 그렇기에 협업 도중 혼동을 불러 일으킬 수 있다.

### let

#### 블록 Scope let

블록은 {}로 바인딩된 코드 청크인데요. 하나의 블록은 중괄호 속에서 존재하며, 중괄호 안에 있는 것은 모두 블록 범위이다.

let으로 선언된 변수는 해당 블록 내에서만 사용가능하다.

```tsx
let greeting = "say Hi";
let times = 4;

if (times > 3) {
  let hello = "say Hello instead";
  console.log(hello); // "say Hello instead"
}
console.log(hello); // hello is not defined
```

중괄호로 감싸진 hello 변수가 정의된 블록 외부에서 helllo를 사용했더니 에러가 반환되는 것을 확인할 수 있다.

#### let은 업데이트될 수 있지만, 재선언은 불가능

var와 마찬가지로 let으로 선언된 변수는 해당 범위 내에서 업데이트될 수 있다.
하지만, var와 달리 let 변수는 범위 내에서 다시 선언할 수 없다.

```tsx
let greeting = "say Hi";
greeting = "say Hello instead";
```

```tsx
let greeting = "say Hi";
let greeting = "say Hello instead"; // error: Identifier 'greeting' has already been declared
```

그러나 동일한 변수가 다른 범위 내에서 정의된다면, 에러는 더 이상 발생하지 않는다.

```tsx
let greeting = "say Hi";
if (true) {
  let greeting = "say Hello instead";
  console.log(greeting); // "say Hello instead"
}
console.log(greeting); // "say Hi"
```

2번째의 코드와 달리 에러가 출력되지 않는 이유는 let은 블록스코프로 두 변수의 범위가 다르기 때문이다.

#### let의 호이스팅

var와 마찬가지로 let 선언은 맨 위로 끌어려진다. undefined(정의되지 않음)으로 초기화되는 var와 다르게 let의 키워드는 초기화되지 않는다. 선언 이전에 let 변수를 사용하려고 시도한다면 Reference Error(참조 오류)가 발생한다.

### Const

#### 블록 Scope const

let 선언처럼 const 선언도 선언된 블록 범위 내에서만 접근 가능하다.

#### const는 업데이트도, 재선언도 불가능

const로 선언된 변수의 값이 해당 범위 내에서 동일하게 유지됨을 의미한다. 업데이트하거나 다시 선언할 수가 없다.

```tsx
const greeting = "say Hi";
greeting = "say Hello instead"; // error: Assignment to constant variable.
```

```tsx
const greeting = "say Hi";
const greeting = "say Hello instead"; // error: Identifier 'greeting' has already been declared
```

따라서 모든 const 선언은 선언하는 당시에 초기화되어야 한다.

개체의 경우는 다소 다른 점이 있다. const 개체는 업데이트할 수 없지만, 개체의 '속성'은 업데이트할 수 있다.

```tsx
const greeting = {
  message: "say Hi",
  times: 4,
};
```

```tsx
greeting.message = "say Hello instead";
```
