# how to use zod

### zod 설치 & 설정

```tsx
yarn add zod
```

zod를 사용할 땐 타입스크립트의 strict 모드를 사용해야 한다.

```tsx
{
  "compilerOptions": {
    "strict": true
  }
}
```

그후 zod를 사용할 파일에서 import하면 된다.

```tsx
import { z } from 'zod';
```

### 스키마 정의

```tsx
const User = z.object({
  email: z.string(),
  age: z.number(),
  active: z.boolean(),
});
```

위와 같이 email은 string, age는 number, active는 boolean으로 설정 할 수 있다.

### 유효성 검증

Zod 스키마를 정의한 후 스키마의 parse() 함수에 넘겨서 유효성을 검사 할 수 있다.

```tsx
User.parse({
  email: 'user@test.com',
  age: 35,
  active: true,
}); // ✅ 유효성 검증 통과

User.parse({
  email: 'user@test.com',
  age: '35',
}); // ❌ 유효성 검증 실패
```

검증이 실패할 경우에는 parse() 함수는 오류(error)를 발생시킨다.

여기서 한 가지 주의할 부분은 검증이 성공했을 경우 parse() 함수가 반환하는 객체에는 검증에 통과한 속성만 포함된다는 것이다. 예를 들어, 다음과 같이 스키마에 정의되지 않은 password 속성을 입력 객체에 포함한 경우,

```tsx
const user = User.parse({
  email: 'user@test.com',
  age: 35,
  active: true,
  password: 'abcd1234',
});

console.log(user);
```

아래와 같이 password가 제외되어 콘솔에 출력된다.

```tsx
{
  email: "user@test.com",
  age: 35,
  active: true,
}
```

### 타입 추론

Zod는 스키마를 기준으로 타입스크립트 타입을 알아서 추론할 수도 있다.

```tsx
interface User {
  email: string;
  age: number;
  active: boolean;
}

function processUser(user: User) {
  User.parse(user); // 유효성 검증
  // 사용자 처리 로직
}
```

Zod의 infer과 자바스크립트의 typeof 연산자를 사용하면 이미 정의한 스키마로 부터 타입을 뽑아낼 수 있다.

```tsx
type User = z.infer<typeof User>;

function processUser(user: User) {
  User.parse(user); // 유효성 검증
  // 사용자 처리 로직
}
```

### 예시 코드

```tsx
import { z } from 'zod';

// Zod 스키마 정의
const User = z.object({
  email: z.string().email(), // 이메일 유효성 검증 추가
  age: z.number().int().positive(), // 나이는 양의 정수로 제한
  active: z.boolean(),
});

// TypeScript 타입 유추
type UserType = z.infer<typeof User>;

// 이메일 발송 모의 함수
function sendWelcomeEmail(email: string) {
  console.log(`Welcome email sent to ${email}`);
}

// 사용자 처리 함수
function processUser(user: UserType) {
  try {
    User.parse(user); // 유효성 검증

    // 사용자 처리 로직
    console.log(`Processing user: ${user.email}`);
    console.log(`Age: ${user.age}`);
    console.log(`Active: ${user.active}`);

    sendWelcomeEmail(user.email);

    console.log('User processed successfully.');
  } catch (error) {
    console.error('User validation failed:', error);
  }
}

// 예시 데이터
const validUser = {
  email: 'user@test.com',
  age: 35,
  active: true,
};

const invalidUser = {
  email: 'user@test.com',
  age: '35', // 잘못된 데이터: 나이가 문자열
};

// 사용자 처리 예시
processUser(validUser); // 유효성 검증 통과 및 처리
processUser(invalidUser); // 유효성 검증 실패
```

#### Zod 스키마 정의

```tsx
const User = z.object({
  email: z.string().email(),
  age: z.number().int().positive(),
  active: z.boolean(),
});
```

#### 사용자 처리 함수

```tsx
function processUser(user: UserType) {
  try {
    User.parse(user); // 유효성 검증

    // 사용자 처리 로직
    console.log(`Processing user: ${user.email}`);
    console.log(`Age: ${user.age}`);
    console.log(`Active: ${user.active}`);

    // 이메일 발송
    sendWelcomeEmail(user.email);

    console.log('User processed successfully.');
  } catch (error) {
    console.error('User validation failed:', error);
  }
}
```

processUser 함수는 입력된 user 객체를 User.parse를 통해 검증하고, 유효할 경우 사용자 정보를 콘솔에 출력하고, 환영 이메일을 발송한다. 유효성 검증에 실패하면 에러 메시지를 출력한다.

#### 사용자 처리 예시

```tsx
const validUser = {
  email: 'user@test.com',
  age: 35,
  active: true,
};

const invalidUser = {
  email: 'user@test.com',
  age: '35', // 잘못된 데이터: 나이가 문자열
};

processUser(validUser); // 유효성 검증 통과 및 처리
processUser(invalidUser); // 유효성 검증 실패
```

예시 데이터를 통해 processUser 함수를 호출하여 유효한 사용자와 유효하지 않은 사용자를 처리하는 과정을 보여준다.
