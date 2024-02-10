# [#2] basic TypeScript types

### boolean
boolean은 참 또는 거짓을 나타낸다.

```ts
const isTypeScriptAwesome: boolean = true;
const doesJavaScriptHasTypes: boolean = false;
```

### number 
number는 숫자를 나타낸다.

```ts
const yourScore: number = 100;
const ieee754IsAwesome: number = 0.1 + 0.2; 
```

### string
string은 문자열을 나타낸다.

```ts
const hisName: string = '이다한';
```

### null/undefined

```ts
const nullValue: null = null;
const undefinedValue: undefined = undefined;
```

## 기타 타입
js에 없는 ts만의 특별한 타입들이 있다.

### any

any 타입은 모든 타입과 호환 가능하다. 

```ts
let bool: any = true;
bool = 3;
bool = 'whatever';
bool = {};
```

any를 남용하면 타입 안정성에 구멍이 뚫린 코드가 되어 타입스크립트를 사용하는 의의가 사라지므로 꼭 필요한 경우에만 사용해야 한다.

### void

void는 null과 undefined 만을 값으로 가질 수 있는 타입이다. 아무런 값도 반환하지 않는 함수의 반환 타입을 표시할 때 사용한다.

```ts
function nothing(): void { }
```

### never 

never는 아무런 값도 가질 수 없는 타입이다. 

```ts
function alwaysThrow(): never {
  throw new Error(`I'm a wicked function!`);
}
```

alwaysThrow 함수는 항상 에러를 throw 하므로 어떤 값도 반환하지 않는다. 이 때, 이런 함수의 반환 타입을 never 타입을 사용해 나타낼 수 있다.