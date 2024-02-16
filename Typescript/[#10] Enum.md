# [#10] Enum

### 숫자 열거형

거형을 정의하며 멤버의 값을 초기화하지 않을 경우, 해당 멤버의 값은 0부터 순차적으로 증가하는 숫자 값을 갖는다.

```jsx
enum Direction {
  TEST1
  TEST2 // 1
  TEST3 // 2
  TEST4 // 3
}
```

```jsx
const TEST: Direction = Direction.TEST3;
console.log(TEST); // 2
```

#### 값을 초기화 한다면?

```jsx
enum InitializedDirection {
  TEST1 = 2,
  TEST2 = 4,
  TEST3 = 8,
  TEST4 = 16
}
```

```jsx
const TEST: Direction = Direction.TEST3;
console.log(TEST); // 8
```

#### 일부만 초기화 한다면?

```jsx
enum InitializedDirection2 {
  TEST1 = 3,
  TEST2 /* 4 */,
  TEST3 = 7,
  TEST4 /* 8 */
}
```

```jsx
const TEST: Direction = Direction.TEST;
console.log(TEST); // 8
```


### 문자열 열거형

```jsx
enum Direction {
  TEST1 = 'TEST1',
  TEST2 = 'TEST2',
  TEST3 = 'TEST3',
  TEST4 = 'TEST4'
}
```
```jsx
const south: Direction = Direction.TEST3;
console.log(TEST); // TEST3
```

#### 주의점

문자열 멤버 이후로 정의된 모든 멤버는 명시적으로 초기화되어야 한다.


### 계산된 멤버

계산된 맴버는 런타임에 결정되는 값을 열거형의 멤버 값으로 사용할 수도 있다. 하지만 계산된 멤버 뒤에 오는 멤버는 반드시 초기화되어야 한다는 점에 유의해야한다.

```jsx
function getAnswer() {
  return 42;
}
enum SpecialNumbers {
  Answer = getAnswer(),
  Mystery // error
```

### 유니온 열거형

유니온 열거형의 멤버는 값인 동시에 타입이 된다. 

```jsx
enum ShapeKind {
  Circle,
  Triangle = 3,
  Square
}
```
```jsx
type Circle = {
  kind: ShapeKind.Circle;
  radius: number;
}
type Triangle = {
  kind: ShapeKind.Triangle;
  maxAngle: number;
}
type Square = {
  kind: ShapeKind.Square;
  maxLength: number;
}
type Shape = Circle | Triangle | Square;
```