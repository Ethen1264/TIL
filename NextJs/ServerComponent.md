# ServerComponent

### React 18 이전의 렌더링

#### CSR

React 18이 나오기 전, 리액트 컴포넌트의 모든 렌더링은 클라이언트 즉, 사용자의 브라우저에서 이루어졌다.

- 서버는 React로 작성한 JavaScript 코드 뭉텅이(이를 번들링이라고 한다)들을 브라우저에게 응답(Response) 한다.
- 브라우저는 응답받은 JavaScript 파일을 해석한 다음 HTML파일로 렌더링하고, 인터랙션이 필요한 Event Listener와 같은 코드들을 장착했다.

#### SSR

Next js의 등장으로 사용할 수 있었다.

- NextJS를 통해서 서버단에서 1)페이지 별로 코드를 쪼갠 후(Code Split), 2) HTML을 렌더링한 다음, 3) 브라우저에게 응답
- 브라우저는 전달 받은 1)HTML을 화면에 보여주고, 2)추가로 내려받은 JS코드들을 연결하는 Hydration 과정을 거친다.

하지만 이때도 브라우저의 기본 랜더링은 CSR이 었고 SSR을 사용할려면 getServerSideProps() 함수와 같은 추가적인 코드 작업이 필요했다.

### React 18 이후의 렌더링

React 18 버전부터 Server Component가 도입되었고 NextJS 13, 즉 App Route 부터 이를 완벽하게 지원한다.

따라서 NextJS App Route 부터는 아래 두가지 형식으로 컴포넌트를 만들 수 있다.

#### server component

- 서버에서 HTML을 렌더링해서 브라우저에게 응답한다.
- Hydration 과정은 없다.

#### client component

- 서버에서 기본적은 HTML은 렌러링해 브라우저에게 응답한다.
- Hydration(JS Interactivity)만 브라우저에서 이루어진다.

기본적은 HTML 자체는 모두 서버에서 렌더링된다!

즉 Client Component라고 할지라도 렌더링은 서버에서 이루어진다, 다만 Hydration은 브라우저에서 일어난다.

Event Listener(클릭 이벤트 등등), Browser API(local storage 등등), React Hooks(useState, useEffect 등등)은 브라우저에서만 작동하는 클라이언트단 JS코드이고, 브라우저에서 Hydration 과정을 거치는 Client Component 에서만 정의될 수 있다.

따라서 Server Component 에서는 사용이 불가능하다.

### Server Component

React Server Component를 사용하면 서버에서 UI를 구성하고 또한 선택적으로 Cached도 할 수 있다.

### Server Rendering의 장점

#### 데이터 패칭

API를 사용해서 데이터를 얻어오는 Date Fetching을 Server Component 코드에서 바로 사용할 수 있다.

이를 통해 렌더링에 필요한 데이터를 가져오는 데 걸리는 시간과 클라이언트가 수행해야 하는 요청(Request) 수를 줄여 성능을 향상할 수 있다.

#### 보안

Server Component는 API Keys 혹은 Token과 같이 민감한 정보 또는 민감한 로직을 클라이언트에게 노출될 위험없이 서버에 보관할 수 있다.

#### 캐싱

서버에서 렌더링하면 결과를 Cached하고 이후에 발생되는 요청 및 사용자 전체에게 재사용할 수 있다.

따라서 성능을 향상시킬 수 있고 동시에 각각의 요청에 따른 데이터 페칭과 렌더링에 들어가는 비용을 아낄 수 있다.

#### 성능

Server Comoponent는 추가적인 성능 최적화가 가능하다.

Server Component를 사용하면 Interactive하지 않은 부분들은 미리 렌더링이 되어있기 때문에 User가 다운로드 받는 JavaScript의 양이 줄어들게 된다.

따라서 User의 Browser에서 JavaScript 다운로드, 파싱, 실행의 부담이 줄어들기 때문에 인터넷 성능이 좋지 않은 단말이나 환경에서도 유리하다.

#### 검색엔진, SNS엔진 최적화

서버에서 미리 렌더링된 HTML은 검색 엔진 봇이 페이지를 확인하고 소셜 네트워크 봇이 페이지에 대한 썸네일을 생성하는 데 사용될 수 있다.

### NextJS에서 Server Component 사용하기

NextJS App Route에서는 기본적으로 Server Component를 사용한다.

따라서 자동적으로 추가적인 작업 없이 서버 렌더링을 구현할수 있고 필요에 따라서 Client Component를 사용할 수 있다.

### 클라이언트 컴포넌트

`use client`는 아래와 같이 사용할 수 있다.

```tsx
"use client";

import { useState } from "react";

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
