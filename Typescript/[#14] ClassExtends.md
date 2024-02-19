# [#14] ClassExtends

인터페이스 확장과 유사하게, 클래스 역시 extends 키워드를 사용해 기존에 존재하는 클래스를 확장할 수 있다. 

- A를 B의 서브클래스(subclass)
- B를 A의 슈퍼클래스(superclass)

서브클래스는 슈퍼클래스의 속성, 메소드를 가지게 된다.

```ts
class Super {
  answer: number = 18;
  Hello() {
    console.log('Hello, world!');
  }
}
class Sub extends Super { }
const sub: Sub = new Sub();
console.log(sub.answer); // 18
sub.Hello(); // Hello, world!
```

### 클래스 확장 시 생성자

슈퍼클래스의 생성자는 서브클래스의 생성자에서 자동 호출되지 않는다. 따라서 서브클래스의 생성자에선 반드시 super 키워드를 사용해 슈퍼클래스의 생성자를 호출해줘야 한다.

```ts
class Base {
  baseProp: number;
  constructor() {
    this.baseProp = 123;
  }
}
class Extended extends Base {
  extendedProp: number;
  constructor() {
    super(); // 반드시 이 호출을 직접 해 주어야 한.
    this.extendedProp = 456;
  }
}
const extended: Extended = new Extended();
console.log(extended.baseProp); // 123
console.log(extended.extendedProp); // 456
```

super() 호출을 하지 않는다면 오류가 발생한다.
만약 생성자가 아닌 그냥 정의를 했다면 super()를 적지 않아도 된다.