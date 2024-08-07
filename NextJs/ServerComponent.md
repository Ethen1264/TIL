# ServerComponent

### 서버 컴포넌트

`서버 컴포넌트` 서버에서 렌더링되는 컴포넌트로 대부분의 컴포넌트가 서버에서 렌더링되고, 작은 인터랙티브 UI 요소만 클라이언트에서 렌더링 되는 방식이다.

`클라이언트 컴포넌트`는 클라이언트에서 렌더링되는 컴포넌트로 Next.js와 같은 프레임워크에서의 서버에서 사전 렌더링되고 클라리언트에서 Hydrate되어 초기 렌더링 성능을 개선할 수 있다.

### 서버 컴포넌트와 SSR(서버 사이드 렌더링)을 같이 사용한다면?

둘다 서버에서 렌더링 된다는 같은 점도 있지만 해결하는 부분이 다르다. 이러한 다른 점을 이용하여 서로 보완하면서 사용할 수 있다.
`서버 사이드 렌더링(SSR)`으로 초기 HTML 페이지를 빠르게 보여주고, `서버 컴포넌트`로는 클라이언트로 전송되는 자바스크립트 번들 사이즈를 감소시킨다면 사용자에게 기존보다 훨씬 빠르게 인터렉팅한 페이지를 제공할 수 있을 것이다.

### 서버 컴포넌트의 장점

- 서버 컴포넌트로 서버 인프라를 더 잘 활용할 수 있다.

- 초기 페이지 로드 속도 증가 및 클라이언트 측 자바스크립트 번들 크기 감소

- 클라이언트 측 런타임을 비동기식으로 로드하여 애플리케이션을 인계하고 상호 작용을 추가할 수 있다.

### 클라이언트 컴포넌트

`use client`는 아래와 같이 사용할 수 있다.

```tsx
'use client';

import { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>Click</button>
    </div>
  );
}
```

이 클라이언트 컴포넌트는 모듈 그래프 내부에 있는 컴포넌트들은 대부분 클라이언트에서 렌더링 되지만 Next.js를 사용하면 서버에서 사전 렌더링되고 클라이언트에서 Hydrate된다.

이러한 클라이언트 컴포넌트도 트징이 있다.

#### 클라이언트 컴포넌트의 특징

- 서버 컴포넌트 모듈 내부에 있는 컴포넌트들은 서버에서만 렌더링된다.
- `use client` 지시문은 다른 것들을 import 하기전에 반드시 파일 제일 상단에 정의되어야 한다.

### 서버 컴포넌트와 클라이언트 컴포넌트의 코드적 차이

#### 클라이언트 컴포넌트

```tsx
"use client";

import { useState, useEffect } from "react";

export default async function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
   const [ topics, setTopics ] = useState();

   useEffect(() => {
  	  const setPage = async () => {
      const { data } = fetch(`http://localhost:9999/topics`);
	  setTopics(data}
    }

    setPage();
  },[])

  return (
    <html>
      <body>
        <ol>
          {topics.map((topic: ITopics) => {
            return (
              <li key={topic.id}>
                <Link href={`/read/${topic.id}`}>{topic.title}</Link>
              </li>
              ...
```

#### 서버 컴포넌트

```tsx
export default async function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  const resp = await fetch(`http://localhost:9999/topics`);
  const topics = await resp.json();

  return (
    <html>
      <body>
        <ol>
          {topics.map((topic: ITopics) => {
            return (
              <li key={topic.id}>
                <Link href={`/read/${topic.id}`}>{topic.title}</Link>
              </li>
              ...
```
