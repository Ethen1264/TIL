# async & await

### promise가 아닌 async await

비동기 작업이란: 특정한 동작이 시작하고 끝날 때 까지 기다리지 않고 나머지 코드를 실행하는 것을 말한다.

비동기 처리는 `웹 페이지의 반응성 향상`, `네트워크 통신`, `병렬 처리`, `에러 처리`라는 장점이 있다.

이러한 비동기 작업을 수행하기 위해선 크게 `callback함수`와 `promise`가 있다. 하지만 이러한 `callback`은 함수가 무한대로 늘어나는 `callback`지옥이 존재한다. 이러한 문제를 해결하고자 `promise`가 등장항였다.

`promise`는 3가지는 상태를 가진다.

- 대기(pending)
- 성공(fulfilled)
- 실패(rejected)

`Promise`는 성공시 `then()`, 실패시 `catch()` 함수를 사용해 성공 상태와 실패 상태시 각각 어떤 동작을 할지 지정할 수 있다.

> 물론.. then에서도 실패 로직을 처리 할 수 있지만 실패시에만 동작하는 catch()두고 then()에서 실패 동작을 처리할 이유가 없다.

아래의 토스페이먼츠 결제 코드를 보면 `promise`가 어떻게 동작하는지 알 수 있다.

```tsx
paymentWidget.requestPayment({
  orderId: "t9JI0Bs1SVdJxRs8yjiQJ",
  orderName: "토스 티셔츠 외 2건",
})
.then(function (data) {
  console.log(data);
	// 성공 처리
})
.catch(function (error) {
	// 에러 처리
  if (error.code == "NEED_CARD_PAYMENT_DETAIL") {
    console.log(error.message);
  }
```

하지만 이러한 `promise`도 콜백과 마찬가지로 `then()` 체인을 길게 이어나가면 콜백 지옥과 같은 문제가 발생한다.

### async & await이란?

위에서 말한 `callback`과 `promise`의 단점을 `async`, `await`으로 보완할 수 있다.

```tsx
async function handleSubmit() {
	...
	return paymentData
	// return Promise.resolve(paymentData) // 위와 같은 결과
}
```

이 코드와 같이 함수 앞에 `async`를 붙이면 `이 함수는 비동기적인 함수이고 Promise를 반환함` 반환값이 `promise`생성 함수가 아니더라도 반환되는 값을 `promise`객체에 넣는 것이다.

그렇다면 `await`은??

`await`은 `async` 함수 안에서 사용할 수 있는 특별한 문법이다. `promise`를 반환하는 함수 앞에 `await`을 붙이면 해당 `promise`의 상태가 바뀔 때 까지 기다린다. 즉 `promise가 성공 상태 또는 실패 상태로 바뀌기 전까지는 다음 연산을 시작하지 않는다`

```tsx
async function handleSubmit() {
  const paymentData = await paymentWidget.requestPayment({
    orderId: "KOISABLdLiIzeM-VGU_8Z", // 주문 ID(직접 만들어주세요)
    orderName: "토스 티셔츠 외 2건", // 주문명
  });
  console.log(paymentData);
  return paymentData;
}
```

위의 코드를 보면 `paymentData`의 상태가 바뀐 후에 `console.log(paymentData);`가 실행된다.

`await`은 `then`과 같은 역할을 한다 그렇기 때문에 콜백 함수를 등록할 필요가 없다.
콜백 함수를 등록할 필요가 없기 때문에 더욱 코드가 간단하다.

또한 예외처리는 `try/catch`를 사용하여 진행하면 된다.

```tsx
async function handleSubmit() {
  try {
    const paymentData = await paymentWidget.requestPayment({
      orderId: "KOISABLdLiIzeM-VGU_8Z", // 주문 ID(직접 만들어주세요)
      orderName: "토스 티셔츠 외 2건", // 주문명
    });
    console.log(paymentData);
    // 성공 처리
    return paymentData;
  } catch (error) {
    // 에러 처리
    console.log(error.message);
  }
}
```
