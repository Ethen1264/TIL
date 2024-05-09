# #4 promiseStaticFunc

### 순차적인 promise의 문제점

```tsx
function getName() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('철수');
      //reject(new Error('에러: 이름이 없어요'));
    }, 1000);
  });
}

function getTodo() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('밥먹기');
      //reject(new Error('에러: 할일이이 없어요'));
    }, 1000);
  });
}

getName()
  .then((name) => {
    console.log(name);
    return getTodo();
  })
  .then((todo) => {
    console.log(todo);
  });
```

위의 코드와 같이 순차적인 promise를 사용하면 철수아 밥먹기가 동작하는데 총 3초가 걸린다. 즉 2번째걸 실행하기 위해선 1번째일이 완료 될 때 까지 기다렸다가 2번째 작업을 해야한다. 만약 위의 두 동작이 병렬도 작동 한다면 2초라는 시간으로 단축할 수 있다.

### promise.all()

```tsx
promise.all([getName(), getTodo()]);
```

이런식으로 코드를 적용하면 getName()이 동작하는 동안 getTodo()도 같이 실행된다. 즉 병렬적으로 처리할 수 있다.

이때 promise.all은 [getName(), getTodo()]이 resolve된다면 새로운 promise를 하나 생성한다.

```tsx
const promise = promise.all([getName(), getTodo()]);
promise
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.log(error);
  });
```

만약 이때 getName(), getTodo() 둘중 하나가 reject 된다면 해당 reject의 메시지를 출력한다. 이때 만약 둘다 reject라면 첫번째의 promise만 보고 판단을 한다. 즉 getName()의 reject를 실행하고 바로 새로 만든 promise도 reject로 지정한다.

### promise.allSettled()

```tsx
const promise = promise.allSettled([getName(), getTodo()]);
```

promise.allSettled는 promise.all과 달리 getName(), getTodo() 둘 중 하나가 reject여도 끝까지 실행한다. 이러한 모든 동작이 끝나면 새로 만든 promise에 각각의 promise의 결과를 출력한다.

### promise.any

```tsx
const promise = promise.any([getName(), getTodo()]);
```

promise.any는 getName(), getTodo()중 가장 먼저 resolve가 된 값을 가지게 된다.

### promise.race

```tsx
const promise = promise.race([getName(), getTodo()]);
```

getName(), getTodo()이 두가지중 가장 먼저 완료된 함수를 찾아 그 함수의 상태를 파악하며 성공시 새로운 promise에 resolve를 실패시 reject를 지정한다.
