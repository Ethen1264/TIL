# copy

### 참조 타입의 복사

참조 타입의 데이터는 복사 시 데이터의 값이 아닌 '값이 저장된 메모리의 주소'가 저장된다.

따라서 참조 타입의 복사 방법은 얕은 복사(Shallow Copy)와 깊은 복사(deep copy)로 나뉜다.

얕은 복사(Shallow copy)는 참조 타입 데이터가 저장한 '메모리 주소 값'을 복사한 것을 의미한다.

깊은 복사(Deep copy)는 새로운 메모리 공간을 확보해 완전히 복사하는 것을 의미한다.

```tsx
let origin = ["a", "b", ["c"]];
let copy = origin.slice();

copy[2].push("d");

console.log(origin); //["a", "b", ["c", "d"]]; // 원본까지 바뀌어버림
console.log(copy); //["a", "b", ["c", "d"]];
```

### 얕은 복사(Shallow Copy)

얕은 복사(Shallow Copy)란 객체를 복사할 때 원본 값과 복사된 값이 같은 참조(=메모리 주소)를 가리키는 것이다.

또한, 객체 안에 객체가 있을 경우에 한 개의 객체라도 원본 객체를 참조한다면 얕은 복사라고 볼 수 있다.

> 얕은 복사 후 해당 변수를 재사용하여 수정한다면 원본 값이 동시에 변하므로 주의가 필요하다.

#### 일반적인 얕은 복사

```tsx
let origin = { name: "Jinny" };
let copy = origin;

copy.name = "Mr.Lee";

console.log(origin.name); // 'Mr.Lee'
console.log(origin === copy); // true
```

#### Object.assign()

Object.assign()을 이용하면 객체 자체는 깊은 복사가 수행되지만, 2차원 이상의 객체는 얕은 복사가 수행된다. 아래 예시에서 객체는 서로 다른 주소를 참조하고 있어 깊은 복사가 이루어졌지만 내부의 객체는 같은 주소를 참조하고 있다.

```tsx
let origin = {
  a: 1,
  b: { c: 2 },
};

let copy = Object.assign({}, origin);
copy.b.c = 3;

console.log(origin === copy); // false
console.log(origin.b.c === copy.b.c); // true
```

#### 스프레드

스프레드도 assign()과 같이 복사한 객체 자체는 깊은 복사이지만 내부의 객체는 얕은 복사가 진행된다.

```tsx
let origin = {
  a: 1,
  b: { c: 2 },
};

let copy = { ...origin };
copy.b.c = 3;

console.log(origin === copy); // false
console.log(origin.b.c === copy.b.c); // true
```

### 깊은 복사(Deep Copy)

깊은 복사(Deep Copy)는 복사된 객체가 다른 주소를 참조하며 내부의 값만 복사된다.

#### 재귀 함수

재귀 함수 isCopyObj를 만든 후 값을 복사한 방법이다.

```tsx
let origin = {
  a: 1,
  b: { c: 2 },
};

function isCopyObj(origin) {
  let res = {};

  for (let key in origin) {
    if (typeof origin[key] === "object") {
      res[key] = isCopyObj(obj[key]);
    } else {
      res[key] = origin[key];
    }
  }

  return res;
}

let copy = isCopyObj(origin);

copy.b.c = 3;
console.log(origin.b.c === copy.b.c); //false
```

#### JSON 객체 이용

JSON.parse()와 JSON.stringify()를 이용한 방법이다.

- stringify() 문법: JSON.stringify() 메소드는 객체를 인수로 받으며 받은 객체는 문자열로 치환
- parse() 문법: JSON.parse() 메소드는 문자열을 인수로 받으며 받은 문자열은 객체로 치환

```tsx
let origin = {
  a: 1,
  b: { c: 2 },
};

let copy = JSON.parse(JSON.stringify(origin));
copy.b.c = 3;

console.log(origin.b.c === copy.b.c); //false
```
