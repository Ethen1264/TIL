# [#1] Why used Typescript

### 1. 오류를 잡기 쉽다.

타입스크립트는 컴파일 언어라고 했는데, 바로 이 컴파일 과정에서 오류를 잡아내기 때문에 오류를 잡아내기 쉽다는 장점이 있다. 자바스크립트는 반면, 실제로 동작하는 과정(런타임 환경)에서 오류를 잡아낼 수 밖에 없다. 


### 2. 타입에 착오가 생기지 않는다.

js는 string과 number가 계산될 정도로 타입이 확실하지 않다. 이렇기에 나중에 본인이 타입을 서로 햇갈려 잘못 계산되는 경우가 종종 발생한다. 이러한 문제를 Ts는 해결할 수 있다.

```js
function add(a, b) {
    return a + b;
}
add(5, "abc"); 
```


### 3. 함수를 잘못 전달할 수 있다.

``` js
function add(num1, num2) {
  console.log(num1 + num2)
}

add();
add(1);
add(1, 2);
add(3, 4, 5);
add('hello', 'world');
```