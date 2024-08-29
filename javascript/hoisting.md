# Hoisting

### 호이스팅이란

인터프리터가 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것을 의미한다. var로 선언한 변수의 경우 호이스팅 시 undefined로 변수를 초기화한다. 하지만 let과 const로 선언한 변수의 경우 호이스팅시 초기화되지 않는다.

### 함수 호이스팅

함수를 호이스팅하는 예시를 보면 호이스팅의 개념을 쉽게 이해할 수 있다.

```tsx
test();

function test() {
  document.writeln('Hoisting');
}

test();
```

함수를 할당하는 `fucntion test(){}` 코드가 함수를 실행하는 `test()` 코드 보다 아래에 작성된 경우, 호이스팅 개념 없인 맨 첫째줄 라인의 `test()`는 실행되지 않아야 한다.

하지만 JS는 함수를 호이스팅 하기 때문에 최상단의 `test()`코드도 정상 작동한다.

#### 함수 호이스팅의 예외

```tsx
test();

const test = function => () {
  document.writeln('Hoisting');
}

test();
```

위와 같이 화살표 함수를 사용하면 위의 함수호스팅 처럼 함수가 실행되는 것이 아닌 `test`는 `함수가 아니다.` 라는 에러가 출력된다.

왜냐하면 실제 실행코드는 아래와 같이 변환되기 때문이다.

```tsx
const test
test = undefined
test()
const test = function => () {
  document.writeln('Hoisting');
}

test();
```

그렇기에 함수가 아닌 상수의 성질을 가지게 된다.

### 변수 호이스팅

#### var

함수 호이스팅과 달리 변수 호이스팅은 `선언, 초기화`만 된채로 호이스팅되고 할당 까지 호이스팅 되지 않는다.

```tsx
console.log(name); // undefined
var name = 'James';
console.log(name); //James
```

그래서 위의 예제에서는 `var name = 'james`가 작성되기 전 `console.log(name)`은 초기화 된 `var name;`을 출력한다는 의미로 `undefined`를 출력하는 것이다.

#### const, var

`const`와 `let`은 `var`의 모호하고 too much로 유연한 문제점을 보완하기 위해 등장한 개념인 만큼 `const`와 `let`으로 변수가 선언되기 이전 라인에 해당 변수를 출력하는 코드를 작성한 경우 `참조 오류`가 발생한다.

```tsx
console.log(name); // ReferenceError
const name = 'James';
console.log(name); // ReferenceError
let name = 'James';
```

하지만 오류가 발생했다고 해서 `const`와 `let으로 선언한 변수는 호이스팅의 예외가 되는 것은 아니다.

여기서 `TDZ(Temporal Dead Zone)`에 대한 개념이 나온다.

### TDZ(Temporal Dead Zone)

```tsx
console.log(name); // ReferenceError: Cannot access 'name' before initialization
let name = 'James';
```

다시 예제로 돌아와서, 최상단 콘솔 로그에서 에러가 발생했기 때문에 `let name="James"`가 호이스팅이 안되는 것으로 보일 수 있다.

단순하게 말하면 호이스팅이 안되는 것이 아니다. `let`, `const`로 선언한 변수는 호이스팅되었지만, 접근만하지 못하게 된 것 이다.

여기서 `console.log(name)`가 작성된 라인, 해당 `zone`을 `일시적으로 죽은 구역`이라고 이해하면 된다. `name`의 선언문이 나오기 전까지는 `name`에 접근할 수 없다는 말이 된다.
