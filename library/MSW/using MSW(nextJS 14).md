# Using MSW(nextJS 14)

### 설치

npm install msw

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

export const handler = [
  http.get('http://www.test.com/test', () => {
    console.log('here');
    return HttpResponse.json({
      success: true,
      message: '성공',
    });
  }),
];
```

#### server.ts

node 환경 설정 파일

```tsx
import { setupServer } from 'msw/node';
import { handler } from './handler';

export const server = setupServer(...handler);
```

layout.tsx에 적용할 component 파일을 생성한다.(NEXT JS 14기준)
src/\_component/msw.component.tsx

```tsx
'use client';

import { useEffect } from 'react';

export const MswComponent = () => {
  useEffect(() => {
    if (process.env.NODE_ENV === 'development') {
      if (typeof window === 'undefined') {
        (async () => {
          const { server } = await import('@/mocks/server');
          server.listen();
        })();
      } else {
        (async () => {
          const { worker } = await import('@/mocks/browser');
          worker.start();
        })();
      }
    }
  }, []);

  return null;
};
```

layout에서 위 컴포넌트를 호출한다.

```tsx
// src/layout.tsx
import { MswComponent } from '@/app/_component/msw.component';

type Props = {
  children: React.ReactNode;
};
export default function RootLayout({ children }: Props) {
  return (
    <html lang="en">
      <body>
        <MswComponent />
        {children}
      </body>
    </html>
  );
}
```

```tsx
.env
NODE_ENV=development
```

마지막으로 터미널에서 서비스 워커를 실행한다.

```tsx
npx msw init public / --save
```

### 실행

```tsx
export default function Main() {
  const submit = async () => {
    const data = await fetch('http://www.test.com/test', {
      method: 'get',
    }).then((res) => {
      return res.json();
    });

    await console.log(data);
  };

  return (
    <>
      <button onClick={submit}>qweqwewqe</button>
    </>
  );
}
```
