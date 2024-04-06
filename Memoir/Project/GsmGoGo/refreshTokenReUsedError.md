## 문제 상황

로그인을 하면 백엔드에서 `accessToken`과 `refreshToken`이 날라와 localStorage에 저장되어 있는 상태였다. 이렇게 저장한 `accessToken`이 만료가 되어 Client에서 통신을 요청을 하면 백앤드에서 403이 날라와 리프래쉬 api를 실행하도록 로직을 만들었다.

```tsx
apiClient.interceptors.response.use(
  (response) => response,
  async (error) => {
    const originalRequest = error.config;

    if (error.response && (error.response.status === 401 || error.response.status === 403)) {
        try {
          const token = localStorage.getItem('refreshToken');
          const response = await axios.get(`${import.meta.env.VITE_CLIENT_API}/auth/refresh`, {
            headers: {
              'Refresh-Token': `${token}`,
            },
          });
          const accessToken = response.headers['authorization'];
          const refreshToken = response.headers['refresh-token'];
          localStorage.setItem('accessToken', accessToken);
          localStorage.setItem('refreshToken', refreshToken);
        } catch (refreshError) {
          window.location.href = '/signin';
          localStorage.removeItem('accessToken');
          localStorage.removeItem('refreshToken');
          return Promise.reject(refreshError);
        }
);
```

하지만 예상과 달리 토큰이 재발급이 된 상태로 catch문이 실행되는 것을 볼 수 있었다. 이유는 만약 통신이 3개가 한 페이지에서 이루어 진다고 쳤을 때 그 통신을 각각 순서대로 A, B, C라고 하자 현재 `accessToken`이 만료되어 있는 상태로 403이 날라온다. 그렇게 되면 A, B, C통신이 모두 `interceptors`되면서 리프래쉬 요청을 보내게 된다. 그러면 먼저 들어간 A가 토큰을 재발급 받아 localStorage에 저장이 된다. 그렇지만 B와 C입장에선 A가 이미 재발급을 해버렸기 때문에 백엔드에서 "이미 사용된 토큰"이라는 말과 함께 404가 날라온다. 그렇기에 토큰이 저장이 된 상태에서 로그인 창으로 리다이렉트 되는 것 이었다.

## 해결방법

- Client에서 만료일을 계산하기
- 통신 대기하기

### Client에서 만료일을 계산하기

제목 그대로 백엔드에게 토큰 만료일을 받아서 토큰이 만료 되면 자동으로 재발급을 시키는 방법이다. 이 방법은 위에 사항처럼 통신으로 재발급 하는 것이 아닌 통신 되기 전 재발급을 시키는 방식이라 위와 같은 이슈가 생기지 않는다. 하지만 백엔드에서 `accessToken`과 `refreshToken`만 날라오고 먼료일은 날라오지 않기 때문에 이 방법은 사용할 수 없다.

### 통신 대기하기

```ts
let isRefreshing = false;
let refreshSubscribers: ((accessToken: string) => void)[] = [];

apiClient.interceptors.response.use(
  (response) => response,
  async (error) => {
    const originalRequest = error.config;

    if (error.response && (error.response.status === 401 || error.response.status === 403)) {
      if (!isRefreshing) {
        isRefreshing = true;
        try {
          const token = localStorage.getItem('refreshToken');
          const response = await axios.get(`${import.meta.env.VITE_CLIENT_API}/auth/refresh`, {
            headers: {
              'Refresh-Token': `${token}`,
            },
          });
          const accessToken = response.headers['authorization'];
          const refreshToken = response.headers['refresh-token'];
          localStorage.setItem('accessToken', accessToken);
          localStorage.setItem('refreshToken', refreshToken);
          originalRequest.headers.Authorization = accessToken;
          refreshSubscribers.forEach((callback) => callback(accessToken));
          refreshSubscribers = [];
          return apiClient(originalRequest);
        } catch (refreshError) {
          window.location.href = '/signin';
          localStorage.removeItem('accessToken');
          localStorage.removeItem('refreshToken');
          return Promise.reject(refreshError);
        } finally {
          isRefreshing = false;
        }
      } else {
        return new Promise((resolve) => {
          refreshSubscribers.push((accessToken) => {
            originalRequest.headers.Authorization = accessToken;
            resolve(apiClient(originalRequest));
          });
        });
      }
    }

    return Promise.reject(error);
  }
);
```

만약 문제 상황처럼 한페이지에서 통신이 2개 이상이 진행되고 순서대로 A, B, C가 있는 상태로 `accessToken`이 만료되어 403이 날라오면 리프래쉬가 진행된다. 이때 A가 리프래쉬를 요청하는 순간 B, C의 동작이 멈추게 된다. 이때 멈추고 있는 통신들은 `refreshSubscribers`라는 배열에 저장된다. 그 후 A가 토큰을 재발급하면 기존의 A의 동작과 `refreshSubscribers` 배열에 저장된 동작이 실행되게 한다.

## 후기

사실 처음에 이 오류를 봤을 때 매우 당황했던 상태였다. 이미 `vercel`로 배포는 된 상태였기 때문이다. 이때 이 글을 본 사람들은 '배포 전에 확인 안 했어?'라는 의문을 가졌을 것이다. 배포 전날 테스트를 했었는데 그때는 `accessToken`이 30분 이었기 때문에 눈치를 채지 못했던 것 이다. 다시 본론으로 돌아와서 나는 해결방법으로 위에서 설명한 `Client에서 만료일을 계산하기`를 생각했다. 하지만 만료일이 날라오지 않는다는 것을 깨달아 다시 고민을 하고 있었다. 이렇게 고민하고 자료를 찾아봐도 아무런 정보를 찾을 수 없어서 내가 직접 코드를 만들었던 것이다.
