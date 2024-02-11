# [#3] Array & Tuple

### 배열

Array 값의 타입을 나타내는데 쓰인다. 원소 타입 뒤에 대괄호([])를 붙여 표현한다.

```ts
const numberArray: number[] = [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55];
const stringArray: string[] = ['a', 'b', 'c'];
```

이 외에도 재내락??을 사용하는 방법이 하나 더 있다.

```ts
const numberArray: Array<number> = [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55];
const stringArray: Array<string> = ['a', 'b', 'c'];
```

### 튜플 

튜플 타입을 이용해 원소의 수와 각 원소의 타입이 정확히 지정된 배열의 타입을 정의할 수 있다.

```ts
const TupleArray: [string, number] = ['이다한', 18]
```

튜플 타입 변수는 정확히 명시된 개수 만큼의 원소만을 가질 수 있다. 