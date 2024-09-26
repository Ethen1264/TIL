# prototype

### 프로토타입이란?

프로토타입은 자바스크립트 객체지향에서 중요한 역할을 한다.
모든 자바스크립트 객체는 프로토타입이라는 숨겨진 속성을 가지고 있으며, 이 속성은 다른 객체를 참조한다. 이 참조된 객체는 해당 객체의 프로토타입으로 불리며, 프로토타입 객체는 속성과 메서드를 포함할 수 있다. 이를 통해 객체는 프로토타입으로부터 속성과 메서드를 상속받을 수 있다.

### 자바스크립트에서 객체 생성과 프로토타입의 관계

사실 위에 정의만 보면 잘 이해가 안되기 때문에.. 코드를 보고 설명하겠다.

```tsx
function 기계() {
  this.q = "strike";
  this.w = "snowball";
}
new 기계();
```

이런식으로 지정을 하면 `{q: 'strike', w: 'snowball'}`이라는 오브잭트가 생성된다.

이렇게 자바스크립트의 모든 객체는 자신의 부모 역할을 하는 객체와 연결되어있고 이 부모 객체를 프로토타입이라고 한다 (사실 prototype은 그냥 부모에게서 물려받은 유전자라고 생각하면 되는데)

```tsx
function 기계() {
  this.q = "strike";
  this.w = "snowball";
}

기계.prototype.name = "kim";

let nunu = new 기계();
```

이런식으로 작성을 한 후 console에 `nunu.name`을 찍어보면 `'kim'`이 출력되는 것을 볼 수 있다.
물론 nunu를 콘솔에 찍어보면 `{q: 'strike', w: 'snowball'}`이게 출력된다.
즉 자식은 `'kim'`을 가지고 있지 않고 부모만 `'kim'`을 가지고 있는 것 이다.

### 프로토타입 체인

```tsx
function 기계() {
  this.q = "strike";
  this.w = "snowball";
}

기계.prototype.name = "kim";

let nunu = new 기계();

console.log(nunu.name);
```

위의 코드처럼 nunu.name을 콘솔에 입력을 하면

1. 직접 자료를 가지고 있다면 그것을 출력
2. 없다면 부모유전자를 검색
3. 계속 부모로 올라가 검색

이러한 과정을 거치게 된다.

### 네이티브 객체 프로토타입

```tsx
let 어레이 = [4, 2, 1];
let 어레이 = new Array(4, 2, 1);
```

1번째 코드로 실행하면 컴퓨터는 2번째 방법으로 변환하여 실행한다.

그렇다면 array.sort()를 사용할 수 있는 이유는 뭘까?

`new Array(4, 2, 1);`라는 배열의 부모의 프로토타입에 `.sort()`가 들어가 있기 때문이다.

### prototype에 접근하기

프토토타입에 접근하기 위해 **proto**(deprecated)를 인스턴스에 사용하거나 Object.getPrototypeOf(instance)를 사용할 수 있다.

```tsx
function Hello(name) {
  this.name = name;
}
const hello = new Hello("hello");
Object.getPrototypeOf(hello) === Hello.prototype; // true
```
