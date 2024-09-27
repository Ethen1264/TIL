# immutability

### 불변성이란?

javascript에서 불변성이란 객체가 생성된 후 그 상태를 변경할 수 없는 것을 뜻한다.
상태를 변경할 수 없는것은 객체의 프로퍼티를 변경할 수 없는 것을 뜻한다.

### Immutable type vs Mutable type

Immutability타입이란 객체의 상태를 변경할 수 없는 것을 뜻한다. 원시 타입은 Immutable type이다. (ex. Number, String, Boolean, Symbol, null, undefined)

```tsx
let a = 1;
a = 2;
console.log(a);
// 2
```

1이라는 변수가 메모리에 할당되고 a를 가리킨다. 그후 a에 2를 할당하면 2라는 값이 새로운 메모리에 할당되고 2를 가리키게 된다. 이때 1은 가비지 컬랙션의 대상이 된다.

### Mutable type은 객체의 상태를 변경할 수 있는 타입이다. (ex. Object, Array, Function)

```tsx
let a = { name: "kim" };
let b = a;

a.name = "lee";

console.log(a);
// { name : "lee" }
console.log(a === b);
// true
```

a라는 객체가 메모리에 할당되었고, b라는 변수가 a를 가리킨다. 그리고 a의 프로퍼티에 'lee'를 반영하면 a와 b 모두 프로퍼티가 'lee'로 변경하게 된다. 왜냐하면 a와 b 모두 같은 객체를 가리키고 있기 때문에, a의 name 프로퍼티를 변경하면 b의 name 프로퍼티도 변경된다.

### 불변성을 유지하는 방법

- Spread Operator (ES6)

```tsx
const obj = { a: 1, b: 2 };
// spread operator (...obj)를 사용하여 obj의 모든 프로퍼티를 복사한다.
const newObj = { ...obj, c: 3 };
console.log(newObj);
// { a: 1, b: 2, c: 3 }
```

- Object.assign

```tsx
const obj = { a: 1, b: 2 };
// Object.assign()을 사용하여 obj의 모든 프로퍼티를 복사한다.
const newObj = Object.assign({}, obj, { c: 3 });
console.log(newObj); // { a: 1, b: 2, c: 3 }
```

depth가 깊어지면, Spread Operator와 Object.assign은 불변성을 유지하려면 많은 코드를 작성해야 한다.

```tsx
const obj = { a: 1, b: 2, c: { d: 3 } };
const newObj = { ...obj, c: { ...obj.c, e: 4 } };
console.log(newObj);
// { a: 1, b: 2, c: { d: 3, e: 4 } }
```

immer 라이브러리를 사용하면, 복잡한 코드 없이 불변성을 유지할 수 있다.

- immer ( immer )

```tsx
import produce from "immer";

const obj = { a: 1, b: 2 };
// immer의 produce()를 사용하여 obj의 모든 프로퍼티를 복사한다.
const newObj = produce(obj, (draft) => {
  draft.c = 3;
});
console.log(newObj);
// { a: 1, b: 2, c: 3 }
```
