# Axios instance & interceptors

### instance가 없는 axios

instace가 없는 axios는 서버와 통신하기 위한 HTTP 비동기 통신 라이브러리이다.

```jsx
const handleSignup = async () => {
  try {
    await axios.post(`${process.env.REACT_APP_CLIENT_API}/signup`, {
      password,
      username,
      nickname,
    });
    navigate('/signin');
  } catch (error) {
    if (password !== checkPw) {
      alert('비밀번호가 일치하지 않습니다.');
    } else if (error.response && error.response.status === 500) {
      alert('중복된 아이디나 이름이 있습니다.');
    } else {
      alert('회원가입에 실패했습니다.');
    }
  }
};
```

axios는 보통 이런식으로 상용된다.

### 이러한 axios의 문제는?

Axios를 사용할 때는 기본적으로 전역 설정이 적용되어 모든 요청에 동일한 설정이 적용된다. 하지만 이는 유연성이 떨어지고, 코드의 가독성과 유지보수성을 해치는 요인이 될 수 있다. 이거를 해결하기 위해 instance를 사용한다.

### axios instace란?

instace는 axios와 같이 HTTP 요청을 보내고 응답을 받는데 사용된다. 하지만 이러한 axios와 달리 독립적인 설정을 적용할 수 있다. 즉, Axios instance 를 사용하면 여러 개의 서로 다른 설정을 가진 인스턴스를 만들어 재사용할 수 있는 것이다.

> 사용법

```jsx
axios.create([config]);
```

```jsx
import axios from 'axios'

const baseURL = 'https://APIURL'
const token = 'testToken'

// 인스턴스 생성
const instance = axios.create({
  baseURL: baseURL,
  timeout: 10000
  headers: {
    'Authorization': `Bearer ${token}`
  }
})

instance.get('/getAPIURL')
  .then((res) => {
    console.log(res.data);
  })
  .catch((err) => {
    console.error(err);
  });
```

### axios instace의 장점

- 여러 API 엔드 포인트를 사용하는 경우 각각에 대한 baseURL 설정
- interceptor, header 등 인스턴스에 한번만 정의하여 중복 피하기
- 코드의 모듈성과 재사용성 높이기

### instace 활용 (interceptors)

axios instace와 interceptors를 사용하여 axios의 응답을 가로챌 수 있다. 즉 A와B가 있을 때 A사이에 들어가 어떠한 동작을 실행하고 B를 실행하게 할 수 있다. 이는 jwt access토큰과 refresh토큰 로직을 만드는데 사용된다.

### interceptors의 문법

interceptors 는 axios.interceptors.request.use 및 axios.interceptors.response.use를 통해 설정할 수 있다.

> 요청 인터셉터

```jsx
axios.interceptors.request.use(
  (config) => {
    // 요청 전에 수행할 작업
    return config;
  },
  (error) => {
    // 요청 오류 처리
    return Promise.reject(error);
  }
);
```

> 응답 인터셉터

```jsx
axios.interceptors.request.use(
  (config) => {
    // 요청 전에 수행할 작업
    return config;
  },
  (error) => {
    // 요청 오류 처리
    return Promise.reject(error);
  }
);
```

> 인터셉터 제거하기
> 특정 상황에 interceptors를 적용하지 않아도 되거나 해당 요청에 대한 추가적인 처리가 필요하지 않을 경우 interceptors 를 제거할 수 있다.

```jsx
const myInterceptor = axios.interceptors.request.use(function () {
  /*...*/
});
axios.interceptors.request.eject(myInterceptor);
```

> instace와 interceptors 조합

```jsx
const instance = axios.create();
instance.interceptors.request.use(function () {
  /*...*/
});
```

```jsx
const instance = axios.create({
  baseURL: `${process.env.REACT_APP_CLIENT_API}`,
  withCredentials: true,
});

instance.interceptors.request.use(async (config) => {
  const tokenManager = new TokenManager();
  const accessTokenIsValid = tokenManager.validateToken(tokenManager.accessTokenExpiresIn, tokenManager.accessToken);
  const refreshTokenIsValid = tokenManager.validateToken(tokenManager.refreshTokenExpiresIn, tokenManager.refreshToken);

  if (!accessTokenIsValid && refreshTokenIsValid) {
    await tokenManager.reissueToken({ refreshToken: tokenManager.refreshToken });
    tokenManager.initToken();
  }

  return config;
});
```

### interceptors의 장점

- 요청과 응답을 가로채 요청이 보내지기 전, 응답이 반환되기 전 특정 작업을 수행
- 여러 요청에 대해 공통된 작업을 수행해 중복 코드 제거
- 요청과 응답에 대한 처리를 자유롭게 확장 가능


### interceptors의 주의점

- interceptors 에 예외 처리하고 처리된 결과를 반환하는 것이 중요하다. 
- interceptors 에서 예외가 발생하면 해당 요청 또는 응답이 실패된다.
- interceptors 설정시 순서에 따라서 요청과 응답 처리 순서가 달라질 수 있기 때문에 조심해야한다.