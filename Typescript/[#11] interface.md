# [#11] interface 

### interface의 형태

interface의 형태는 type과 엄청 유사하다.

```ts
interface User {
  name: string;
  age: number;
}
```

또한 읽기 전용과 선택 속성을 지정할 수 있다.

```ts
interface User {
  name: string;
  readonly age: number;
  favoriteLanguage?: string;
}
const author: User = { name: '안희종', age: 36 }; // favoriteLanguage가 선택 속성이라 없어도 괜찮다.
author.age = 40; // age가 읽기 전용이라 수정이 불가능하다.
```

### 함수 인터페이스
함수의 타입을 정의할 때도 사용된다.

```ts
interface SquareFunc {
  (num: number): number;
}
const squareFunc: SquareFunc = function (num: number) {
  return num * num;
}

console.log(squareFunc(10)); // 10
```

### 제너릭 인터페이스

```ts
interface Dropdown<T> {
    value: T;
    selected: boolean;
}
const obj: Dropdown<string> = { value: 'abc', selected: false }
```