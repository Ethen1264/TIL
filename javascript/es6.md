# es6

### ES6 (ECMAScript 2015)

1. `let`과 `const`: 블록 스코프 변수를 선언 할 수 있다.

```tsx
let a = 10;
const b = 20;
```

2. 화살표 함수: 함수 표현을 간결하게 한다.

```tsx
const sum = (x, y) => x + y;
```

3. 템플릿 리터럴: 문자열을 포함해 더 쉽게 변수나 표현식을 표현할 수 있다.

```tsx
const name = "John";
const greeting = `Hello, ${name}!`;
```

4. 디스트럭처릴 할당: 객체나 배열의 값을 쉽게 추출 할 수 있다.

```tsx
const person = { name: "John", age: 30 };
const { name, age } = person;
```

5. 기본 매개변수: 함수 매개변수에 기본값을 설정할 수 있다.

```tsx
function greet(name = "Guest") {
  console.log(`Hello, ${name}`);
}
```

6. 나머지 매개변수: 여러 인수를 배열로 받을 수 있다.

```tsx
function sum(...numbers) {
  return numbers.reduce((acc, curr) => acc + curr, 0);
}
```

7. 스프레드 문법: 배열이나 객체를 쉽게 복사하거나 병합할 수 있다.

```tsx
const arr = [1, 2, 3];
const arrCopy = [...arr];
```

8. 모듈: `import`와 `export`를 사용해 모듈 간에 기능을 공유할 수 있다.

```tsx
// module.js
export const foo = 42;

// main.js
import { foo } from "./module.js";
```

9. 클래스: 객체 지향 프로그래밍을 위한 문법이 추가되었다.

```tsx
class Person {
  constructor(name) {
    this.name = name;
  }
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}
```

10. promise: 바동기 작업을 처리하기 위한 방법을 제공한다.

```tsx
const fetchData = () =>
  new Promise((resolve) => {
    setTimeout(() => resolve("Data received"), 1000);
  });
fetchData().then((data) => console.log(data));
```

### ES7 (ECMAScript 2016)

1. 지수 연산자: \*\*을 사용해 지수 계산을 할 수 있다.

```tsx
console.log(2 ** 3); // 8
```

2. `Array.prototype.includes`: 배열에 특정 요소가 포함되어 있는지 확인한다.

```tsx
const arr = [1, 2, 3];
console.log(arr.includes(2)); // true
```

### ES8 (ECMAScript 2017)

1. `async`와 `await`: 비동기 프로그래밍을 더 직관적으로 작성할 수 있다.

```tsx
const fetchData = async () => {
  const data = await fetch("https://api.example.com");
  return data.json();
};
```

2. `Object.entries`, `Object.values`, `Object.keys`: 객체의 키, 값, 키-값 쌍을 배열로 반환한다.

```tsx
const obj = { a: 1, b: 2 };
console.log(Object.entries(obj)); // [['a', 1], ['b', 2]]
```

### ES9 (ECMAScript 2018)

1. `Rest/Spread` 속성: 객체에도 나머지/스프레드 문법을 사용할 수 있다.

```tsx
const obj = { a: 1, b: 2, c: 3 };
const { a, ...rest } = obj;
console.log(rest); // { b: 2, c: 3 }
```

2. 비동기 이터레이터: `for-await-of`로 비동기 데이터를 반복 처리할 수 있다.

```tsx
async function process(data) {
  for await (let item of data) {
    console.log(item);
  }
}
```

### ES10 (ECMAScript 2019)

1. `Array.prototype.flat` 및 `flatMap`: 다차원 배열을 평탄화할 수 있다.

```tsx
const arr = [1, [2, 3], [4, 5]];
console.log(arr.flat()); // [1, 2, 3, 4, 5]
```

```tsx
const numbers = [1, 2, 3, 4];

// 각 숫자에 대해 배열을 생성한 후, 이를 평탄화
const result = numbers.flatMap((num) => [num, num * 2]);

console.log(result);
// [1, 2, 2, 4, 3, 6, 4, 8]
// ----------------------------------------------------------
const resultWithMap = numbers.map((num) => [num, num * 2]);

console.log(resultWithMap);
// [[1, 2], [2, 4], [3, 6], [4, 8]]
```

2. `Object.fromEntries`: `Object.entries`와 반대 동작을 수행해 배열을 객체로 변환합니다.

```tsx
const arr = [
  ["a", 1],
  ["b", 2],
];
const obj = Object.fromEntries(arr);
console.log(obj); // { a: 1, b: 2 }
```

```tsx
const person = {
  name: "Alice",
  age: 25,
  city: "Seoul",
};

const entries = Object.entries(person);
console.log(entries);
// [['name', 'Alice'], ['age', 25], ['city', 'Seoul']]
```

3. Optional Catch Binding: `catch` 문에서 매개변수를 생략할 수 있다.

```tsx
try {
  // Some error-prone code
} catch {
  console.log("Error occurred");
}
```

### ES11 (ECMAScript 2020)

1. Null 병합 연산자 (??): `null` 또는 `undefined`인 경우에만 기본값을 반환한다.

```tsx
const name = null ?? "Guest";
console.log(name); // Guest
```

2. Optional Chaining (?.): 존재하지 않는 속성에 접근할 때 에러 없이 `undefined`를 반환한다.

```tsx
const user = {};
console.log(user?.profile?.name); // undefined
```

3. Promise.allSettled: 모든 프로미스가 해결되거나 거부될 때까지 기다린 후 결과를 반환한다.

```tsx
const promises = [Promise.resolve(1), Promise.reject("Error")];
Promise.allSettled(promises).then((results) => console.log(results));
```

4. BigInt: 매우 큰 정수를 표현할 수 있다.

```tsx
const bigInt = 123456789012345678901234567890n;
```

### ES12 (ECMAScript 2021)

1. String.prototype.replaceAll: 문자열 내 모든 일치 항목을 치환할 수 있다.

```tsx
const text = "foo foo foo";
console.log(text.replaceAll("foo", "bar")); // bar bar bar
```

2. `Logical Assignment Operators`: 논리 연산과 할당을 한번에 할 수 있다.

```tsx
let x = true;
x &&= false; // x = x && false;
```

### ES13 (ECMAScript 2022)

1. `at()` 메서드: 배열의 인덱스에서 요소를 가져오는 새로운 방식. 음수 인덱스를 지원

```tsx
const arr = [1, 2, 3];
console.log(arr.at(-1)); // 3
```

2. `Top-level await`: 모듈의 최상위에서 `await`을 사용할 수 있다.

```tsx
const data = await fetch("https://api.example.com");
```

### ES14 (ECMAScript 2023)

1. `Array.prototype.findLast` 및 `findLastIndex`: 배열에서 조건을 만족하는 마지막 요소와 그 인덱스를 찾는 메서드

```tsx
const arr = [1, 2, 3, 4, 5];
const lastEven = arr.findLast((x) => x % 2 === 0); // 4
```

2. `Array.prototype.toSorted`, `toReversed`, `toSpliced`: 기존 배열을 변경하지 않고 정렬, 반전, 또는 요소를 삭제한 새 배열을 반환하는 메서드

```tsx
const sortedArr = arr.toSorted(); // [1, 2, 3, 4, 5]
const reversedArr = arr.toReversed(); // [5, 4, 3, 2, 1]
const splicedArr = arr.toSpliced(1, 2, 6); // [1, 6, 4, 5]
```
