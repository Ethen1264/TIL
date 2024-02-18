# [#12] interfaceExtends

Extends를 사용하여 interface를 상속 시킬 수 있다.

```ts
interface User {
  name: string;
  readonly height: number;
  favoriteLanguage?: string;
}

interface LoggedInUser extends User {
  loggedInAt: string;
}

const macbook15: LoggedInUser = { name: 'Ethen', height: 30, loggedInAt: 'eadazcadwq123q' };
```

이런식으로 User에만 있는 값들을 LoggedInUser에 상속하여 LoggedInUser에 쓸 수 있다.

### 다수의 인터페이스 상속

인터페이스들은 반점(,)으로 구분하여 상속 시킬 수 있다.

```ts
interface ElectricDevice {
  voltage: number;
}
interface SquareShape {
  width: number;
  height: number;
}
interface Laptop extends ElectricDevice, SquareShape {
  color: string;
}
const macbook15: Laptop = { voltage: 220, width: 30, height: 21; color: 'white' };
```