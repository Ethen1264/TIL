# [#8] Union

### 유니온 타입을 쓰면??

하나의 타입을 제외하고 모든 부분이 똑같은데도 여러번 써야 해 비효율적일 때
어떤 타입이 가질 수 있는 경우의 수를 나열하여 사용하는 유니온 타입으로 이 함수의 반환 타입을 표현할 수 있다.

### 사용법

유니온 타입은 가능한 모든 타입을 파이프(|) 기호로 이어서 표현한다.

```ts
type SquaredType = string | number;
function square(value: number, returnOnString: boolean = false): SquaredType {
  /* 본문 동일 */
}
```

```ts
type Whatever = number | string | boolean;
```
