# [#13] Class

### 클래스의 형태

```ts
class Test {}
```

이렇게 정의된 클래스는 new를 이용해 instantiation(인스턴스화) 할 수 있다.

```ts
const test: Test = new Test();
```

이렇게 Test라는 클래스를 정의할 때, 이름은 같지만 의미는 다른 두 식별자가 동시에 생성된다.

- 타입 Test: Test 클래스 인스턴스의 타입 (const test: Test)
- 함수 Test: new 키워드와 함께 호출되는 클래스 Test의 `생성자` (new Test())

const test: Test = new Test() 라는 코드에서 앞의 Test는 인스턴스의 타입을 가리키는 반면, 뒤의 Test는 해당 클래스의 `생성자`, 즉 함수 타입의 값이다.

### 생성자

constructor 키워드를 사용해 클래스 생성자를 정의할 수 있다. 만약 어떤 클래스가 생성자를 정의하지 않았다면, 본문이 비어있는 함수가 생성자로 사용된다. (constructor() {} ) 객체 생성자와 유사하게, 클래스 생성자를 통해 클래스 인스턴스가 생성될 때 실행될 로직을 정의할 수 있다.

```ts
class Hello {
  constructor() {
    console.log('hi!');
  }
}
const hello: Hello = new Hello(); // 콘솔에 hi!가 출력됨
```

생성자는 임의의 매개변수를 취할 수 있다. 이 변수들은 클래스를 인스턴스화 할 때 인자로 넘겨진다.

```ts
class Id {
  constructor(Id: string) {
    console.log(`${Id}!`);
  }
}

const id: Id = new Id('Ethen1264'); // Ethen1264!
```

만약 생성자에서 정의한 Id가 string이 아닌 number와 같은 다른 경우가 온다면 에러가 발생한다.

### 속성

클래스 인스턴스도 속성을 가질 수 있다. 클래스 내에서는 속성엔 this 키워드를 이용해 접근 가능하다. 모든 클래스 속성은 ```이름: 타입``` 형태로 표시 해야한다.

```ts
class User {
  // 속성 선언
  age: number;
  constructor() {
    // 속성 할당
    this.age = 18;
  }
}
const user: User = new User();
console.log(user.age); // 18
```

### 읽기 전용

class도 type과 인터페이스와 마찬가지로 ```readonly 키워드를 사용해 읽기 전용 속성으로 바꿀 수 있다. 하지만 속성 선언 또는 생성자 외의 장소에서는 읽기 전용 속성에 값을 할당 할 수 없다.

```ts
class User {
  // 속성 선언
  readonly age: number;
  constructor() {
    // 속성 할당
    this.age = 18;
  }
}
const user: User = new User();
user.age = 17; // error readonly로 되어있음
```

이때 readonly 속성은 꼭 한번은 값이 정해져 있어야 한다.

### 메소드

객체의 단축 메소드명과 유사한 문법을 사용해 인스턴스의 메소드를 정의할 수 있다. 메소드 내에서는 this 키워드를 사용해 해당 메소드가 호출되는 인스턴스를 참조할 수 있다.

```ts
class Age {
  age: number;
  
  constructor(age: number) {
    this.age = age;
  }
  
  ageNumber(): void {
    console.log(`${this.age}!`);
  }
}
const age: age = new age('18');
Age.ageNumber(); // 18!
```