# spread 문법

### 의미 

spread의 사전적 의미는 펼치다.라는 뜻을 가지고 있다. 즉 이 문법을 사용한다면 

- 객체 리터럴의 프로퍼티 목록
- 배열 리터럴의 요소 목록
- 함수 호출문의 인수 목록

이와 같은 상황에서 값들을 펼질 수 있다.

### 객체 리터럴

``` jsx
const car = {
  name: '자동차'
};

const tire = {
  ...car,
  size: 'big'
};

const color = {
  ...tire,
  color: 'purple'
};

console.log(car);   // 자동차
console.log(tire);  // 자동차, big
console.log(color); // 자동차, big, purple
```

### 배열

``` jsx
var arr = [1,2,3,4];
console.log(arr); // [1, 2, 3, 4]

const arr2 = [...arr, 5, 6];
console.log(arr2);  // [1, 2, 3, 4, 5, 6]
```

``` jsx
const arr = [1, 2, 3, 4, 5];

const maxNum = Math.max(...arr);

console.log(maxNum); // 5
```