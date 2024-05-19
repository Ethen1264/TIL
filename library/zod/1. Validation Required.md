# Why Validation Is Required

### 유효성 검사가 필요한 이유

#### account.ts

```tsx
interface Account {
  id: string;
  email: string;
  age: number;
  level: 'GOLD' | 'SILVER' | 'BRONZE';
  active: boolean;
  createdAt: Date;
  image?: string | undefined;
  ips?: string[] | undefined;
}

function processAccount(account: Account) {
  // 어떤 로직
}
```

그 다음 Account 인터페이스와 일치하지 않는 인수로 processAccount() 함수를 호출하려고 하면 아래와 같이 타입 에러가 발생한다.

#### account.test.ts

```tsx
processAccount({}); // ❌ Argument of type '{}' is not assignable to parameter of type 'Account'.

processAccount({
  id: 101, //  ❌ Type 'number' is not assignable to type 'string'.ts(2322)
  email: 'user@test.com',
  age: '35', //  ❌ Type 'string' is not assignable to type 'number'.ts(2322)
  level: 'PLATINUM', //  ❌ Type '"PLATINUM"' is not assignable to type '"GOLD" | "SILVER" | "BRONZE"'.ts(2322)
  active: true,
  createdAt: '2020-01-17T16:45:30', //  ❌ Type 'string' is not assignable to type 'Date'.ts(2322)
});
```

위에서 작성한 타입스크립트 코드를 타입스크립트 tsc를 통해서 자바스크립트로 변환하면?
Account 인터페이스가 없어지고, processAccount() 함수에 붙어있던 타입 정보도 모두 사라지게 된다.
그러므로 이 함수를 실제로 호출할 때는 어떤 형태의 인수를 넘기더라도 아무런 문제가 발생하지 않는다.

```tsx
updateAccount({}); // ✅ 문제없이 실행 됨

updateAccount({
  id: 101,
  email: 'user@test.com',
  age: '35',
  level: 'PLATINUM',
  active: true,
  createdAt: '2020-01-17T16:45:30',
}); // ✅ 문제없이 실행 됨
```

이를 통해 우리는 아래와 같은 사실을 알 수 있다.

> 1. 타입스크립트 코드에서 타입 에러는 컴파일 과정에서만 발생할 수 있다.
> 2. 실제로 자바스크립트 프로그램이 실행될 때는 타입스크립트는 아무런 역할을 못한다.

### 타입 시스템의 한계

외부에서 들어오는 데이터를 효과적으로 검증하려면 단순히 자료형을 제한하는 것만으로는 부족할 때가 많다. 예를 들어, 자바스크립트에서는 숫자형과 문자형을 구분지을 수는 있지만 숫자형 내에서 정수와 실수를 구분할 수는 없고 숫자의 범위를 제한할 수도 없다. 문자형을 데이터를 입력받을 때도 정해진 선택지 내에서 입력을 받고 싶거나 이메일, URL, IP 등 특정 문자열 형식으로 입력을 받아야 할 수도 있다.

```tsx
interface Account {
  id: string;
  email: string;
  age: number;
}

processAccount({
  id: '', // ⚠️ 빈문자열
  email: 'https://www.daleseo.com', // ⚠️ 이메일 형식에 맞지 않음
  age: 9999.123, // ⚠️ 9999살? 나이가 소수?
});
```

실제로 애플리케이션에 요구하는 유효성 검증은 자바스크립트의 느슨한 타입 시스템으로 충족하기에는 한계가 있다. 이러한 현실적인 이유로 대부분의 애플리케이션에서는 타입스크립트 사용과 별개로 유효성 검증을 구현하게 된다.

### 유효성 검증 구현의 고통

```tsx
interface Account {
  id: string;
  email: string;
  age: number;
  level: 'GOLD' | 'SILVER' | 'BRONZE';
  active: boolean;
  createdAt: Date;
  image?: string | undefined;
  ips?: string[] | undefined;
}

function updateAccount(account: Account) {
  if (typeof account.id !== 'string' || account.id.length < 36) throw new Error('Invalid id');

  if (typeof account.age !== 'number' || account.age < 0) throw new Error('Invalid age');

  if (!['GOLD', 'SILVER', 'BRONZE'].includes(account.level)) throw new Error('Invalid level');

  if (!(account.createdAt instanceof Date)) throw new Error('Invalid createdAt');

  // 어떤 로직
}
```

위의 코드와 같이 직접 유효성 검증 구현을 할시 개발 생산성이나 유지 보수 측면에서 효과적인 접근 방법이 아니다.

### 유효성 검증 라이브러리

대표적으로 Joi와 Yup, Zod들이 있다. 이 유효성 검증 라이브러리들은 공통적으로 타입스크립트가 아닌 자바스크립트로 스키마(schema)를 정의하고 이것을 이용하여 유효성 검증을 가능하게 해준다.

```tsx
// ✅ 스키마 정의
const Account = z.object({
  id: z.string().uuid(),
  email: z.string().email(),
  age: z.number().int().min(18).max(80),
  level: z.enum(['GOLD', 'SILVER', 'BRONZE']),
  image: z.string().url().max(200).optional(),
  ips: z.string().ip().array().optional(),
  active: z.boolean().default(false),
  createdAt: z.date().default(new Date()),
});

// ✅ 스키마로 부터 타입 추론
type Account = z.infer<typeof Account>;

function updateAccount(account: Account) {
  // ✅ 스키마로 유효성 검증
  Account.parse(account);

  // 어떤 로직
}
```

이렇게 라이브러리를 사용하면 좀 더 깔끔한 코드를 만들 수 있다.
