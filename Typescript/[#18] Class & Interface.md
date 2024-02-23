# [#18] Class & Interface

### 클래스의 인터페이스 구현

인터페이스는 본질적으로 값이 어떤 멤버를 반드시 가져야 하며 그 멤버들의 타입은 어때야 한다는 제약을 나타내는 수단이다. implements 키워드를 사용해 클래스가 이러한 제약을 따라야 함을 표현할 수 있다. 아래 코드를 보자.

```ts
interface Animal {
  legs: number;
}

class Dog implements Animal {}
```

아래와 같은 오류가 발생한다.

```ts
error TS2420: Class 'Dog' incorrectly implements interface 'Animal'.
  Property 'legs' is missing in type 'Dog'.
```

Animal 인터페이스에 legs라는 값이 number가 존재해야 하는데 존재하지 않기 때문에 에러가 발생한다.
아래와 같이 수정하면 에러가 발생하지 않는다.

```ts
interface Animal {
  legs: number;
}

class Dog implements Animal {
  legs: number = 4;
}
```

### 인터페이스의 클래스 확장

인터페이스가 기존에 존재하는 클래스의 형태를 확장하는 것 또한 가능하다. 인터페이스 확장과 유사하게 extends 키워드를 사용해 클래스를 확장할 수 있다.

```ts
class Point {
    x: number;
    y: number;
}

interface Point3d extends Point {
    z: number;
}

const point3d: Point3d = {x: 1, y: 2, z: 3};
```

위 코드처럼 Point3d 인터페이스는 자신의 z: number 속성 이외에도 Point 클래스의 멤버인 x: number, y: number 속성을 가진다.