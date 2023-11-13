# Axios

## Axios란??

- Axios는 브라우저, Node.js를 위한 Promise API를 활용하는 HTTP 비동기 통신 라이브러리이다.
- 쉽게 말해서 backend, frontend 통신을 쉽게 하기 위해 Ajax와 더불어 사용한다.
- 자바스크립트에는 fetch api 가 있지만, 프레임워크에서 ajax를 구현할때는 axios를 쓴다.

## Axios의 특징

- 운영 환경에 따라 브라우저의 XMLHttpRequest 객체 또는 Node js의 http api 사용
- 요청과 응답 데이터의 변형
- HTTP 요청 취소
- HTTP 요청과 응답을 JSON 형태로 자동 변경

## Axios 설치

```
yarn add axios
```

### 문법구성

```jsx
axios({
  url: 'https://test/api/cafe/list/today', // 통신할 웹문서
  method: 'get', // 통신할 방식
  data: {
    // 인자로 보낼 데이터
    foo: 'diary',
  },
});
```

- method : 요청방식. (get이 디폴트)
- url : 서버 주소
- baseURL : url을 상대경로로 쓸대 url 맨 앞에 붙는 주소.
  예를들어, url이 /post 이고 baseURL이 https://some-domain.com/api/ 이면,
  https://some-domain.com/api/post로 요청 가게 된다.
- headers : 요청 헤더
- data : 요청 방식이 'PUT', 'POST', 'PATCH' 해당하는 경우 - - body에 보내는 데이터
- params : URL 파라미터 ( ?key=value 로 요청하는 url get방식을 객체로 표현한 것)
- timeout : 요청 timeout이 발동 되기 전 milliseconds의 시간을 요청. timeout 보다 요청이 길어진다면, 요청은 취소되게 된다.
- responseType : 서버가 응답해주는 데이터의 타입 지정 (arraybuffer, documetn, json, text, stream, blob)
- responseEncoding : 디코딩 응답에 사용하기 위한 인코딩 (utf-8)
- transformRequest : 서버에 전달되기 전에 요청 데이터를 바꿀 수 있다.
- 요청 방식 'PUT', 'POST', 'PATCH', 'DELETE' 에 해당하는 경우에 이용 가능
- 배열의 마지막 함수는 string 또는 Buffer, 또는 ArrayBuffer를 반환합
- header 객체를 수정 가능
- transformResponse : 응답 데이터가 만들어지기 전에 변환 가능
- withCredentials : cross-site access-control 요청을 허용 유무. 이를 true로 하면 cross-origin으로 쿠키값을 전달 할 수 있다.
- auth : HTTP의 기본 인증에 사용. auth를 통해서 HTTP의 기본 인증이 구성이 가능
- maxContentLength: http 응답 내용의 max 사이즈를 지정하도록 하는 옵션
- validateStatus : HTTP응답 상태 코드에 대해 promise의 반환 값이 resolve 또는 reject 할지 지정하도록 하는 옵션
- maxRedirects : node.js에서 사용되는 리다이렉트 최대치를 지정
- httpAgent / httpsAgent : node.js에서 http나 https를 요청을 할때 사용자 정의 agent를 정의하는 옵션
- proxy : proxy서버의 hostname과 port를 정의하는 옵션
- cancelToken : 요청을 취소하는데 사용되어 지는 취소토큰을 명시

### axios 응답

axios를 통해 요청을 서버에게 보내면, 서버에서 처리를하고 다시 데이터를 클라이언트에 응답 하게 된다.
이를 .then으로 함수인자로(response)로 받아 객체에 담진 데이터가 바로 응답 데이터이다.

```jsx
axios({
  method: 'get', // 통신 방식
  url: 'www.naver.com', // 서버
}).then(function (response) {
  console.log(response.data);
  console.log(response.status);
  console.log(response.statusText);
  console.log(response.headers);
  console.log(response.config);
});
```

## Axios 단축 메소드

```jsx
axios.request(config)

axios.get(url[, config])

axios.delete(url[, config])

axios.head(url[, config])

axios.options(url[, config])

axios.post(url[, data[, config]])

axios.put(url[, data[, config]])

axios.patch(url[, data[, config]])
```

## axios GET

- get 메서드에는 2가지 상황이 크게 존재한다.
  - 단순 데이터(페이지 요청, 지정된 요청) 요청을 수행할 경우
  - 파라미터 데이터를 포함시키는 경우 (사용자 번호에 따른 조회)

```jsx
// user에게 할당된 id 값과 함께 요청을 합니다.
axios
  .get('/user?ID=12345')
  .then(function (response) {
    // 성공했을 때
    console.log(response);
  })
  .catch(function (error) {
    // 에러가 났을 때
    console.log(error);
  })
  .finally(function () {
    // 항상 실행되는 함수
  });
// 위와는 같지만, 옵션을 주고자 할 때는 이렇게 요청을 합니다.
axios
  .get('/user', {
    params: {
      ID: 12345,
    },
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  })
  .finally(function () {
    // always executed
  });

// async/await 를 쓰고 싶다면 async 함수/메소드를 만듭니다.
async function getUser() {
  try {
    const response = await axios.get('/user?ID=12345');
    console.log(response);
  } catch (error) {
    console.error(error);
  }
}
```

## axios Post

post 메서드에는 일반적으로 데이터를 Message Body에 포함시켜 보낸다.

위에서 봤던 get 메서드에서 params를 사용한 경우와 비슷하게 수행된다.

```jsx
axios
  .post('url', {
    firstName: 'Fred',
    lastName: 'Flintstone',
  })
  .then(function (response) {
    // response
  })
  .catch(function (error) {
    // 오류발생시 실행
  });
```

## axios Delete

delete 메서드에는 일반적으로 body가 비어있다.

REST 기반 API 프로그램에서 데이터베이스에 저장되어 있는 내용을 삭제하는 목적으로 사용한다.

```jsx
axios
  .delete('/user?ID=12345')
  .then(function (response) {
    // handle success
    console.log(response);
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  });
```

하지만 query나 params가 많아져서 헤더에 많은 정보를 담을 수 없을 때는

다음과 같이 두 번째 인자에 data를 추가해줄 수 있다.

```jsx
axios
  .delete('/user?ID=12345', {
    data: {
      post_id: 1,
      comment_id: 13,
      username: 'foo',
    },
  })
  .then(function (response) {
    // handle success
    console.log(response);
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  });
```

## axios Put

API 프로그램에서 데이터베이스에 저장되어 있는 내용을 갱신(수정)하는 목적으로 사용된다..

PUT메서드는 서버에 있는 데이터베이스의 내용을 변경하는 것을 주 목적으로 하고 있다.

put 메서드는 서버 내부적으로 get -> post 과정을 거치기 때문에 post 메서드와 비슷한 형태이다.

```jsx
axios
  .put('url', {
    username: '',
    password: '',
  })
  .then(function (response) {
    // response
  })
  .catch(function (error) {
    // 오류발생시 실행
  });
```

PATCH는 PUT과 비슷한 느낌이지만 PUT과 다르게 리소스의 일부분만 수정할 수 있다.

PATCH 메소드는 PUT 메소드와 달리 먹등성을 가지지 않는데, 이는 동일한 patch 요청이 다른 결과를 야기할 수 있음을 뜻한다.

## CallBack

1. 콜백 : 다른 함수에 인수로 넘겨주는 함수. 호출(call back)되어 실행(execute)될 목적으로 인수로 넘기는 함수이다.
setTimeout(콜백함수, 지연시간ms) : 특정시간 이후 콜백함수를 

2. 실행한다. clearTimeout(함수명)을 통해 스케줄링을 취소할 수 있다.

setTimeout을 통해 이전 함수의 처리 결과를 기다린 후, callback을 실행시키는 방식으로 비동기 처리를 구현할 수 있다.

## 동기(Sync), 비동기(Async)란?

![Alt text](/img/image-14.png)

### ✅ 동기(synchronous = 동시에 일어나는)

: 이전 작업이 끝나야 다음 작업이 실행된다.
요청과 그 결과가 동시에 일어난다는 약속이며, 요청을 하면 시간이 얼마나 걸리든지 요청한 자리에서 결과가 주어져야 한다.

> 설계가 매우 간단하고 직관적이지만,
결과가 주어질 때 까지 아무것도 하지 못하고 대기해야한다.

✅ 비동기(Asynchronous = 동시에 일어나지 않는)

: 이전 작업 수행 중에도 다른 작업을 수행할 수 있게 하는 것 (작업이 순차적으로 실행되지 않는다)
요청한 결과가 동시에 일어나지 않을거라는 약속이다.

> 동기 방식보다 복잡하지만,
결과가 주어지는데 시간이 걸리더라도 그 시간 동안 다른 작업을 할 수 있기 때문에 자원을 효율적으로 사용할 수 있다.

## 비동기 작업의 결과는 어떻게 처리할까?

### - 동기 작업은 직관적

이전 실행의 결과가 나오면, 그 다음 실행을 하기 때문에
어떤 작업의 순서를 정하고 싶다면 순차적으로 코드를 적기만 하면 된다.

### - 비동기 작업은 ?

선행된 작업이 끝나지 않았음에도 다음 작업이 시작된다.

만약 비동기 작업의 결과를 그 다음 작업에 사용하고 싶다면? 비동기 작업과 그 이후 작업을 마치 동기 작업처럼 동작하도록 만들어줘야 한다.

`promise` , `async` , `await` 키워드를 사용하여 비동기 작업을 마치 동기적으로, 즉 비동기 작업이 끝난 후 특정 작업들을 실행할 수 있도록 순서를 정해주는 것이다.


### promise
promise객체는 `비동기 작업이 끝난 후 결과를 알려주는 용도` 로 사용한다.
promise를 사용하면, 비동기 작업이 끝난 시점을 알 수 있어 동기 작업처럼 구성할 수 있게 된다.

`대기` , `이행`, `거부` 총 3개의 상태를 갖는다.
`각각 작업 완료 전`, `작업 완료 후`, `에러 발생하여 실패` 라는 뜻이다.

- promise 사용 방법
비동기 작업이 작업 종료 후, promise 객체를 반환하도록 하고
promise 객체가 제공하는 then, catch를 이용하면 된다.

``` jsx 
const promise = // promise를 반환하는 어떤 비동기 작업...
      
promise.then((result) => console.log('성공!').catch((error) => console.log('실패..')
```

promise 객체에 `.then`을 붙이면 이행 상태의 처리를 할 수 있다.
`.catch`를 붙이면 실패 상태를 처리할 수 있다.

### await 

`promise` 객체를 사용하더라도 `.then()`, `.catch()` 등등 뒤에 붙이는 것들이 많아진다.

이러한 키워드를 붙이지 않고, 더욱 간단하게 비동기 작업을 동기적으로 만들어주는 키워드가 `await` 이다.

- await 사용 방법
비동기 작업 앞에 await 키워드를 붙이면, 비동기 작업이 결과를 낼 때까지 기다린다.

  - 여기서 기다린다는 의미는, 모든 작업이 종료될 때까지 기다린다는 의미가 아니다.
  - 내가 사용할 결과값이 나올 때까지 기다린다는 의미이다.

  - 즉, 메인 작업들은 멈추지 않고 await를 포함하고 있는 함수만 일시정지된다.

    > await는 혼자 쓸 수 없다 = async 키워드와 함께 사용한다.

### async
async는 특정 함수를 비동기로 만드는 키워드이다.

await와 세트로 사용하는 이유는,

비동기 작업을 포함하고 있기 때문에 그 함수도 비동기여야 한다.
await으로 그 함수만 일시정지하므로, 결국 이 것도 비동기이다.
동기적으로 처리할 일이 있는 비동기 작업에 await를 붙이고, 해당 작업을 포함하고 있는 함수에 async를 붙이면 된다.

``` jsx
const getData = async() => {
	const {data:result} = await axios.get("server adress");
    return result;
}
```

만약 이것을 그냥 비동기 통신으로 수행한다면, result 에 아무런 값이 없는 상태에서 무언가가 처리된다. 그러나 비동기 통신을 동기적으로 수행하고자 await을 붙였으니, 서버에 데이터를 받아오는 동안에는 작업이 일시중지된다. 그리고 서버에 결과를 받아오고 나서야 Result 에 값이 들어간다.