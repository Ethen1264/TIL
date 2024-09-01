# Closure

### 클로저란?

클로저란 `함수와 함수가 선언되었을 때의 렉시컬 환경의 조합`이다.

- 클로저란, 자신이 `선언된 당시의 환경`을 기억하는 함수이다.
- 클로저란, 생명 주기가 끝난 `외부 함수의 변수`에 `접근`할 수 있는 내부 함수이다.

```tsx
function outerFunc() {
  // 외부 함수의 변수
  var x = 10;

  // 내부 함수에서 외부 함수의 변수에 접근할 수 있습니다.
  var innerFunc = function () {
    console.log(x);
  };

  return innerFunc;
}

var inner = outerFunc();
inner(); // 10
```

위의 코드에서 outerFunc는 내부 함수 innerFunc를 반환하고 종료 되었다. 이로인해 outerFunc가 호출된 후에는 내부 변수 x도 유효하지 않을 것이라고 생각할 수 있다. 하지만 inner 함수를 호출하면 내부 함수 innerFunc가 실행되고, innerFunc는 선언된 당시의 환경을 기억하고 있기 때문에 (내 상위 스코프에는 var x가 선언 됐었지..) 변수 x의 값인 10이 출력됩된다.

이처럼 `생명 주기가 끝난 외부 함수의 변수에 접근`할 수 있는 함수를 `클로저`라고 한다.

### 선행지식

#### 스코프

- 변수에 접근할 수 있는 범위를 뜻한다. 자바스크립트에는 전역 스코프와 지역 스코프가 있다

#### 렉시컬 스코프

함수를 어디에 선언 하였는지에 따라 상위 스코프가 결정되는 것 이다. 이를 정적 스코프라고 부르기도 한다.

```tsx
var x = 1;

function foo() {
  var x = 10;
  bar();
}

function bar() {
  console.log(x);
}

foo(); // 1
bar(); // 1
```

foo 함수 안에서 호출된 bar 함수는 전역 변수 x와 지역 변수 x중 변수 x이다.

렉시컬 스코프는 호출이 아니라 선언에 집중한다.
bar 함수는 전역에 선언되었기 때문에 전역 변수 x를 참조하게 되는 것이다.

### 동작원리

- 클로저는 자신이 선언되었을 때의 환경(=렉시컬 스코프)를 기억 하는 함수이다.
- 자바스크립트의 모든 함수는 Environment라 불리는 숨김 프로퍼티를 가지고 있다. 이곳에 렉시컬 스코프에 대한 참조값이 저장된다.
- 함수 본문에서 Environment를 상요해서 외부 함수의 변수에도 접근할 수 있다.

#### 쉽게 이해하기

- 클로저 = `함수` + `렉시컬 스코프`
- 자바스크립트의 모든 함수는 자신이 선언된 환경의 주소를 저장하고 있다. 즉 상위 스코프의 주소를 가지고 있는 것이다.
- 함수 본문에서 상위 스코프의 주소를 참조하여 외부 함수의 변수에도 접근할 수 있게 된다.

### 클로저를 사용하는 이유

#### 상태 유지

- 현재 상태를 기억하고 변경된 최신 상태를 유지할 수 있다.

```tsx
function debounce(callback, delay) {
  let timer = null;

  return function () {
    clearTimeout(timer);
    timer = setTimeout(() => {
      callback.apply(this, arguments);
    }, delay);
  };
}
```

- 익명 함수는 debounce 내에서 선언되었으므로 debounce 함수가 상위 스코프가 된다.
- 함수는 선언된 환경의 주소를 기억하기 때문에 상위 스코프의 변수에 접근할 수 있게 되고, timer 변수에 접근할 수 있게 된다.
- timer는 디바운스가 실행될 함수와 다른 스코프에 있기 때문에 timer에 대한 최신 상태를 유지할 수 있다.

#### 정보 은닉

- 변수 값을 은닉 할 수 있다. 즉 객체지향 class의 private 처럼 사용할 수 있다.

#### 전역 변수 사용 억제

- 프로그래밍 초보자들은 전역 변수를 통해서 공유할 변수를 작성하고는 한다. 하지만 전역 변수는 의도치 않게 값이 변경될 위험이 있다.
- 클로저를 사용하면 변수를 공유하는 특성은 유지하되 데이터를 은닉화할 수 있기 때문에, 전역 변수를 대체하여 안전한 코드를 작성할 수 있다.

```tsx
const btn = document.querySelector("button");

btn.addEventListener("click", handleClick);

let count = 0;
function handleCilck() {
  count++;
  return count;
}
```

위의 코드는 count를 전역변수로 사용해줘야 count가 증가한다.
이럴때 클로저를 사용할 수 있다.

```tsx
const btn = document.querySelector("button");

btn.addEventListener("click", handleClick());

function handleCilck() {
  let count = 0;
  return function () {
    count++;
    return count;
  };
}
```

위와 같이 작성해 준다면 외부함수(handleClick)의 lexical environment를 참조하는 함수를 btn의 콜백함수로 이용해 전역객체 없이 구현할 수 있다.

### 클로저와 React의 useState

#### useState 구현하기

```tsx
function useState(initialValue) {
  // 클로저를 통해 상태 값 유지
  let state = initialValue;

  // 상태 값을 반환하고 상태를 업데이트하는 함수
  function setState(newValue) {
    state = newValue;
  }

  // 현재 상태 값과 상태 업데이트 함수를 반환
  return [() => state, setState];
}

// 사용 예시
const [count, setCount] = useState(0);

console.log(count()); // 0
setCount(1);
console.log(count()); // 1
```

- useState 함수

  - useState 함수의 초기화 코드는 단 한 번만 실행된다.
  - 즉, let state = initialValue;와 return [() => state, setState];는 useState가 호출될 때 딱 한 번만 실행된다.
  - 이후 count()나 setCount()를 호출할 때는 이 초기화 코드가 다시 실행되지 않고, 클로저를 통해 유지된 state 값에 접근하거나 그 값을 변경하는 동작만 수행된다.

- console.log(count()); // 0 실행

  - count()는 useState 함수가 반환한 () => state 함수이다.
  - 이 함수가 실행되면, 이미 초기화된 state 값을 반환한다.
  - 이때 state는 useState가 처음 호출되었을 때 설정된 값인 0이므로, count()는 0을 반환하게 된다.
  - 따라서 console.log(count());는 0을 출력한다.

- setCount(1) 실행 과정

  - setCount(1) 호출:

    - setCount(1)을 호출하면 setState 함수가 실행됩니다.
    - setState 함수는 state = newValue; 코드를 실행하여 state 값을 인자로 받은 1로 변경합니다.

  - 클로저를 통한 상태 업데이트:

    - 중요한 점은 setState 함수가 useState의 내부에 정의되어 있고, useState 호출 시 초기화된 state 변수를 클로저로 기억하고 있다는 점이다.
    - 이 덕분에 setState 함수는 외부에서 호출되더라도 state 변수를 접근하고 변경할 수 있다.
    - state는 useState 함수가 호출될 때 초기화된 이후에도 setState가 변경할 때마다 최신 값을 유지하게 된다.

  - 상태 변경 후:

    - setCount(1)이 호출되면 state가 0에서 1로 업데이트된다
    - 이후 count()를 호출하면 업데이트된 state 값인 1을 반환하게 된다

### 주의할 점

- 클로저를 사용하면 메모리 측면에서 손해를 볼 수 있다.
  - 클로저에 의해 내부 함수는 외부 함수의 변수를 참조하고 있다.
  - 라서 외부 함수의 생명 주기가 끝났음에도 가비지 콜렉터에 의해 메모리가 해제되지 않는다.

#### 해결 방법

- 클로저를 할당한 변수에 null을 할당해줌으로써 메모리를 해제시키는 방법이 있다.
