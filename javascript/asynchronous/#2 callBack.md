# #2 callBack

### 콜백 함수란?

다른 함수의 인자로 전달되는 함수를 말한다. 예를 들어서

```tsx
function main(callback) {
  callback();
}

main(function () {});
```

이 코드에선 `function () {}` 이 부분이 콜백 함수가 된다.

### 비동기 콜백이란?

비동기적인 작업은 정확히 언제 끝나는지 알 수 없다. 또한 코드가 동기적이지 않기에 코드의 실행 순서를 특정하지 못한다.

그런데 만약 특정 비동기작업이 완료 된 후 후처리가 진행되어야 한다면 콜백 함수를 적용하면 된다.

#### 콜백함수 적용 전

```tsx
function getData() {
  setTimeout(() => {
    console.log('서버에서 데이터를 받아왔어요');
  }, 2000);
}

getData();
console.log('후처리...');
```

```
후처리... //바로 실행됨

서버에서 데이터를 받아왔어요 //2초 후에 실행됨
```

```tsx
function getData(callback) {
  setTimeout(() => {
    console.log('서버에서 데이터를 받아왔어요');
    callback();
  }, 2000);
}

getData(() => {
  console.log('후처리...');
});
```

```
서버에서 데이터를 받아왔어요 //2초 후에 실행됨
후처리... //2초 후에 실행됨
```
