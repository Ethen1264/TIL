# [#15] ClassStatic

클래스 전체에서 공유되는 값이 필요한 경우, 스태틱 멤버를 사용할 수 있다. 스태틱 멤버에는 클래스 이름을 사용해 접근 할 수 있다.

### 스태틱 속성

속성 선언 앞에 static 키워드를 붙여 스태틱 속성을 정의할 수 있다.

```ts
class User {
  static count: age = 18;
}
console.log(User.age); // 18
```

### 스태틱 메소드 

메소드 선언 앞에 static 키워드를 붙여 스태틱 메소드를 정의 할 수 있다.

```ts
class User {
  static age: number = 17;
  static increaseAge() {
    User.age += 1;
  }
  static getAge() {
    return User.age;
  }
}
User.increaseAge();
console.log(User.getAge()); // 18
User.increaseAge();
console.log(User.getAge()); // 19
```