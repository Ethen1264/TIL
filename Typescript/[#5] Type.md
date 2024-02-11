# [5] Type

### 타입의 형태

```ts
type NewType = Type;
```
타입은 보통 이런식으로 정의 하는데 타입 자리엔 기본 타입을 포함한 모든 타입이 올 수 있다.

```ts
type Age = number;
type Height = number;
type AnotherAge = Age;
type Animals = Animal[];
type User = {
  name: string;
  height: number;
};
```

이 때 별칭은 단순히 새로운 이름을 붙일 뿐이고, 실제로 새로운 타입이 생성되는 것이 아니다. 예를 들어, 아래와 같은 코드의 에러 메시지에는 Age 대신 number 이 사용된다.

```ts
type Age = number;
function getUser(uuid: Age) {
  /* 함수 본문 */
}
getUser('hi'); // error Age는 넘버를 지칭하기 때문에 함수의 값은 string이 아닌 number가 되어야 한다.
```