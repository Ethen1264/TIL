# Zustand

### react 상태관리란?

프론트엔드에서 상태는 렌더하는데 있어서 영향을 미칠 수 있는 값을 뜻한다.
상태를 어떻게 관리하느냐에 따라 웹을 렌더하는데 영향을 미칠 수 있다. 프론트엔드 개발자에게 상태관리는 중요한 임무가 되었다.
리액트는 부모 -> 자식으로 `props`를 전달하여 상태를 공유? 할 수 있다. 하지만 이러한 `props` 전달 방식은 프로젝트의 규모에 따라 힘들어질 수 있다. 그렇기에 이러한 문제를 해결하기 위해 `zustand`와 같은 상태관리 라이브러리가 등장 하였다.

### Zustand란?

Zustand란 상태라는 뜻을 가진 독일어이다.

1. 이름 뜻도 쉽지만 사용방법 또한 매우 쉽다.
   바닐라 자바스크립트를 기준으로 핵심 로직의 코드 줄 수가 약 42줄밖에 되지 않는다.

2. 상태가 변경되면 불필요한 리렌더링을 일으키지 않는다.

3. 보일러플레이트가 거의 없다.
   보일러플레이트란 최소한의 변경으로 여러 곳에서 재사용되며 반복적으로 비슷한 형태를 띄는 양상을 말한다.

### Zustand 설치

```
npm install zustand
```

```
yarn add zustand
```

### Zustand 예시

```jsx
import React from 'react';
import create from 'zustand';

// Zustand store
const useCounterStore = create((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 })),
  decrement: () => set((state) => ({ count: state.count - 1 })),
  reset: () => set({ count: 0 }),
}));

const Counter = () => {
  const { count, increment, decrement, reset } = useCounterStore();

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
};
```

![](https://velog.velcdn.com/images/ethen1264/post/78899293-8e3f-45f2-999f-fb5168fa9214/image.png)

위 코드는 위 이미지와 같이 랜더링 된다.

`useCounterStore`를 선언하여 초기 count값을 0으로 선언한다. 또 `inrement` 와 `decrement`, `reset` 함수를 만든다. 그후 `useCounterStore`를 사용하여 위에서 만든 것들을 가지고 와서 사용한다.
