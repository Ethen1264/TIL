# [#6] Function

### 함수의 타입

함수는 크게 두가지 타입이 있다.

>

- 매개변수(parameter)의 타입
- 반환값(return value)의 타입 (반환 타입)

  >

- 매개변수의 경우, 매개변수 뒤에 콜론(:)을 붙이고 타입을 적는다. (param1: number)

- 반환 타입은 매개변수 목록을 닫는 괄호())와 함수 본문을 여는 여는 대괄호({) 사이에 콜론을 붙이고 표기한다. (function (): number { ... })

```ts
function sum(a: number, b: number): number {
  return a + b;
}

//sum(a: number, b: number)은 a와b에 각각 number라는 값이 들어간다는 이야기 이고 : number{}는 return 값이 number일거라는 이야기 이다.
```

만약 리턴값이 필요없다면 void를 사용한다.

```ts
function A(name: string): void {
  console.log(name);
}
```

만약 void를 지정을 했는데 return값이 있다면 오류가 발생한다. 마찬가지로 number로 지정을 했는데 return하지 않는다면 오류가 발생한다.

### 화살표 함수

```ts
const sum = (a: number, b: number): number => {
  return a + b;
};
```

### 함수 값의 타입 표기

함수 타입의 값에 타입 표기를 붙이기 위해서는 화살표 함수 정의 문법과 비슷한 문법을 사용한다.

```ts
(...매개변수 나열) => 반환 타입
```

매개변수가 없는 함수의 경우 매개변수를 생략해 아래와 같이 적는다.

```ts
() => 반환 타입
```

화살표 함수 문법을 사용한 함수 또한 비슷하게 정의 가능하다.

```ts
const yetAnotherSum: (a: number, b: number) => number = sum;
const onePlusOne: () => number = () => 2;
const arrowSum: (a: number, b: number) => number = (a, b) => a + b;
```

### 기본 매개변수

타입스크립트에서도 기본 매개변수 문법을 사용할 수 있다.

```ts
매개변수명: 타입 = 기본값;
```

이런 형태로 사용한다.

```ts
function Hello(name: string = 'Ethen'): void {
  console.log(`Hello, ${name}`);
}
greetings('Fuyu'); // Hello, Fuyu!
greetings(); // Hello, Ethen!
```

### 선택 매개변수

많은 프로그래밍 언어는 함수 정의에 명시된 매개변수의 수보다 많거나 적은 수의 인자가 들어온 경우 에러를 뱉는다. 한편, 자바스크립트는 더 들어온 인자는 버리고, 덜 들어온 인자는 undefined가 들어온 것과 동일하게 취급한 후 어떻게든 함수를 실행하려 시도한다. 물론 타입스크립트의 보호를 받는것이 좋을 때도 있지만 불필요한 경우도 있다. 이럴경우 `?`를 붙혀 해결할 수 있다. 예를들어 `optional?: number`이런식으로 말이다.

```ts
function user(name: string, age?: number): void {
  if (age === null) {
    console.log('그의 이름은' + name + '이다.');
  } else {
    console.log('그의 이름은' + name + '이고 나이는' + age + '이다.');
  }
}
user('이다한', 18);
user('이다한');
```

이 때 매개변수 정의 순서에서 선택 매개변수 이후에 필수 매개변수를 두는 것은 허용되지 않는다.

```ts
function user(age?: number, name: string): void {
  if (age === null) {
    console.log('그의 이름은' + name + '이다.');
  } else {
    console.log('그의 이름은' + name + '이고 나이는' + age + '이다.');
  }
}
user('이다한', 18); //error
user('이다한'); //error
```

### 함수 오버로딩

- 함수는 하나 이상의 타입 시그니처를 가질 수 있다.
- 함수는 단 하나의 구현을 가질 수 있다.

즉, 오버로딩을 통해서 여러 형태의 함수 타입을 정의할 수 있지만, 실제 구현은 한 번만 가능하므로 여러 경우에 대한 분기는 함수 본문 내에서 이루어져야 한다.

```ts
function doubleString(str: string): string {
  return `${str}${str}`;
}
function doubleNumber(num: number): number {
  return num * 2;
}
function doubleBooleanArray(arr: boolean[]): boolean[] {
  return arr.concat(arr);
}
```

이렇게 불필요한 함수를 여러가지를 만드는 것이 아닌

```ts
function double(str: string): string;
function double(num: number): number;
function double(arr: boolean[]): boolean[];

const num = double(3); // number
const str = double('ab'); // string
const arr = double([true, false]); // boolean[]
```

이런식으로 적용할 수 있다. 이렇게 하면 타입이 알아서 올바른 함수에 들어가게 된다.

