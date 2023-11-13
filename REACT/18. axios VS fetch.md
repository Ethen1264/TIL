# [React] axios 와 fetch 차이점

흔히 우리는 백엔드 또는 서드파티 API에 네트워크 요청이 필요한 애플리케이션을 개발할 때 Axios 및 Fetch와 같은 HTTP 클라이언트를 사용합니다.

## Fetch 및 Axios에 대한 간략한 개요

Fetch API는 네트워크 요청을 위해 fetch()라는 메서드를 제공하는 인터페이스입니다. 모던 브라우저에 내장되어 있어 따로 설치할 필요가 없습니다. node.js의 실험적 기능을 활성화하여 사용할 수 있습니다.

Axios는 서드파티 라이브러리로 CDN 혹은 npm 이나 yarn과 같은 패키지 매니저를 통해 설치하여 프로젝트에 추가할 수 있습니다. Axios는 브라우저 혹은 node.js 환경에서 실행할 수 있습니다.

Fetch 와 axios는 모두 promise 기반의 HTTP 클라이언트입니다. 즉 이 클라이언트를 이용해 네트워크 요청을 하면 이행(resolve) 혹은 거부(reject)할 수 있는 promise가 반환됩니다.

## Axios 설치하기

  1. NPM을 사용하여 설치
  ```
  npm install axios
  ```

  2 Yarn을 사용하여 설치
  ```
  yarn add axios
  ```

  그 후 프로젝트에서 import 해야합니다.
  
  ```jsx
  import axios from "axios";
  ```

  만약 브라우저에서 Axios를 사용한다면 아래와 같이 CDN을 사용할 수 있습니다.

  ```jsx
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  ```

## Fetch와 Axios의 기능 비교

### 문법

Fetch는 두 개의 인자를 받습니다. 첫 번째 인자는 가져오고자 하는 리소스의 URL입니다. 두 번째 인자는 요청의 설정 옵션을 포함하는 객체로 선택적 인자입니다.

두 번째 인자로 설정 옵션을 넘기지 않을 경우, 기본적으로 GET 요청을 생성합니다.

```jsx
fetch(url);
```
설정 옵션을 넘기면 다음과 같이 요청에 대해 커스텀 설정을 할 수 있습니다.

```jsx
fetch(url, {
  method: "GET", // 다른 옵션도 가능합니다 (POST, PUT, DELETE, etc.)
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({}),
});
```

---

Axios의 문법도 비슷하나, 다양한 방법으로 요청할 수 있습니다.
```jsx
axios(url, {
  // 설정 옵션
});
```

아래와 같이 HTTP 메서드를 붙일 수도 있습니다.

```jsx
axios.get(url, {
  // 설정 옵션
});
```

fetch 메서드처럼 HTTP 메서드 없이 요청할 경우 기본적으로 GET 요청을 생성합니다

```jsx
axios(url);
```

또, 두 번째 인자를 사용해서 커스텀 설정하는 것도 가능합니다.

```jsx
axios(url, {
  method: "get", // 다른 옵션도 가능합니다 (post, put, delete, etc.)
  headers: {},
  data: {},
});
```

```jsx
axios({
  method: "get",
  url: url,
  headers: {},
  data: {},
});
```

