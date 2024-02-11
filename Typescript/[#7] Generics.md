# [#7] Generics

### 제네릭을 쓰는 이유

- 제네릭이 없는 경우

```ts
function getSize(arr: number[] | string[] | boolean[]): number {
  return arr.length;
}

const arr1 = [1, 2, 3];
getSize(arr1);
const arr2 = ['a', 'b', 'c'];
getSize(arr2);
const arr3 = [false, true, false];
getSize(arr3);
```

또는 any 타입을 사용해야한다.

```ts
function getSize(arr: any): number {
  return arr.length;
}

const arr1 = [1, 2, 3];
getSize(arr1);
const arr2 = ['a', 'b', 'c'];
getSize(arr2);
const arr3 = [false, true, false];
getSize(arr3);
```

any를 쓰는 것은 함수의 arg가 어떤 타입이든 받을 수 있다는 점에서 제네릭이지만, 실제로 함수가 반환할 때 어떤 타입인지에 대한 정보는 잃게 된다. 즉 any를 사용하면 ts의 보호에서 벗어나게 된다. 그렇기에 제네릭을 사용해야한다.

```ts
function getSize<T>(arr: T[]): number {
  return arr.length;
}

const arr1 = [1, 2, 3];
getSize<number | string>(arr1);
const arr2 = ['a', 'b', 'c'];
getSize<string>(arr2);
const arr3 = [false, true, false];
getSize<boolean>(arr3);
getSize(arr3);
```

### interface에서 사용하는 법

```ts
interface Mobile<T> {
  name: string;
  price: number;
  option: T;
}

const m1: Mobile<object> = {
  name: 's21',
  price: 1000,
  option: {
    color: 'red',
    coupon: false,
  },
};

const m2: Mobile<string> = {
  name: 's20',
  price: 900,
  option: 'good',
};
```

### 두 개 이상의 제네릭 사용하기

```ts
  const useMultipleGeneric = <T, U> (v:T, u:U): [T, U] => {
    return [v, u];
  }

  useMultipleGeneric('string', 123)
```

두 변수의 타입이 다를 경우 두 가지의 타입 변수가 필요하다. 이 때 제네릭을 사용할 수 있다. 관용적으로 사용하는 T 다음으로 오는 알파벳을 순서대로 사용하면 된다.