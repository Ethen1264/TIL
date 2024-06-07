# Using MSW(react)

### 설치

```
npm install msw
```

```tsx
npx msw init public / --save
```

### 폴더

src 폴더 하위에 mocks 폴더를 생성한다.

![alt text](/img/mocks.png)

browser.ts, handler.ts,

### 설정

#### browser.ts

브라우저 환경 설정 파일

```tsx
import { setupWorker } from 'msw/browser';
import { handler } from './handler';

export const worker = setupWorker(...handler);
```

#### handler.ts

요청을 mocking하는 파일

```tsx
import { http, HttpResponse } from 'msw';

export const handlers = [
  http.get('/api/users', () => {
    return HttpResponse.json([
      {
        id: 1,
        name: 'test',
      },
    ]);
  }),
];
```

#### .env

```tsx
NODE_ENV = development;
```

#### index.ts

```tsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';

async function enableMocking() {
  if (process.env.NODE_ENV !== 'development') {
    return
  }

  const { worker } = await import('./mocks/browser')
  return worker.start()
}


enableMocking().then(()=> {
  ReactDOM.createRoot(document.getElementById('root') as HTMLElement).render(
    <React.StrictMode>
      <App />
  </React.StrictMode>
  )
```

### 실행하기

```tsx
useEffect(() => {
  fetch('/api/users')
    .then((res) => res.json())
    .then((data) => console.log(data));
}, []);
```
