# [#16] ClassAccessModifier

접근 제한자를 사용하여 인스턴스의 맴버에 대한 접근을 권한에 따라 제한 할 수 있다. 이러한 접근 제한자에는 아래와 같은 종류가 있다.

- public
- private
- protected

### public 

public은 제한이 아무것도 존재하지 않아 프로그램의 어느 곳이든 접근이 가능하다. 또한 접근 제한자가 표시되지 않은 맴버는 모드 public으로 칭한다.

```ts
class User {
  age: number;
  
  constructor() {
    this.age = 3;
  }
}

class User {
  public age: number;
  
  public constructor() {
    this.age = 3;
  }
}
```

### private 

private는 해당 클래스의 내부에서만 접근이 가능하며 상속받은 자식도 접근이 불가능 하다. 만약 해당 클래스의 외부에서 접근하게 된다면 에러가 발생한다.

```ts
class User {
  private password: string;
  
  constructor (password: string) {
    this.password = password;
  }
}

const Ethen = new User('1234');
console.log(Ethen.password); //error 
```

private 멤버의 접근 제한은 서브클래스에도 적용된다. 기본적으로 서브클래스는 슈퍼클래스의 멤버에 접근할 수 있지만, 만약 해당 멤버가 private 멤버라면 접근할 수 없다.

```ts
class CarOwner extends User {
  carId: string;
  
  constructor (password: string, carId: string) {
    super(password);
    this.carId = carId;
  }
  
  setPassword(newPassword: string) {
    this.password = newPassword;
    error
  }
 }
 ```

 ### protected

 protected 권한의 멤버는 private과 비슷하게 동작하지만, 서브클래스에서의 접근 또한 허용된다는 점이 다르다.

 ```ts
 class User {
  protected password: string;
  
  constructor (password: string) {
    this.password = password;
  }
}

class CarOwner extends User {
  carId: string;
  
  constructor (password: string, carId: string) {
    super(password);
    this.carId = carId;
  }
  
  setPassword(newPassword: string) {
    this.password = newPassword;
  }
}
```