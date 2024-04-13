# [#1] Recoil

### Recoil이란?

Recoil React 상태 관리 라이브러리로 React는 기본적으로 단방향 데이터 흐름을 따르기 때문에 복잡한 상태 관리를 위해서는 상태를 끌어올리거나 Redux와 같은 상태 관리 라이브러리를 사용해야 했다. 하지만 Recoil은 기존 React 컴포넌트 내에서 상태를 관리할 수 있게 되었다.

### Recoil 설치

#### yarn

```
yarn add recoil
```

#### npm

```
npm i recoil
```

### RecoilRoot

만약 `Recoil`을 사용하고 싶다면 사용할 컴포넌트를 `RecoilRoot`로 감싸야한다.

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import { RecoilRoot } from 'recoil';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <RecoilRoot>
      <App />
    </RecoilRoot>
  </React.StrictMode>
);
```

위의 예시는 APP.js에 그대로 리코일을 사용할 예정 이었기 때문에 app 컴포넌트를 감쌌다.

### Atom

```jsx
import { atom } from 'recoil';

export const countState = atom({
  key: 'count',
  default: 10,
});
```

`atom` 은 store 와 유사한 개념으로, 상태의 단위 이다.
atom이 업데이트 되면, 해당 atom을 구독하고 있던 모든 컴포넌트들의 state가 새로운 값으로 재
렌더링 된다.

### useRecoilState

```jsx
import './App.css';
import { useRecoilState } from 'recoil';
import { countState } from './Atom';

function Counter() {
  const [count, setCount] = useRecoilState(countState);
  return (
    <div>
      <h1>Counter</h1>
      <button
        onClick={() => {
          setCount(count + 1);
        }}
      >
        +
      </button>
      {count}
    </div>
  );
}

function DisplayCounter(props) {
  const [count] = useRecoilState(countState);
  return <div>{count}</div>;
}

function App() {
  return (
    <div>
      <Counter />
      <DisplayCounter />
    </div>
  );
}

export default App;
```

`useRecoilState` hook은 atom의 state를 get 그리고 set 할 수 있다.

```jsx
const [count, setCount] = useRecoilState(countState);
```

다음과 같이 사용하면, count 는 countState value를 가지게 되고

setText는 text의 값을 변경할 수 있다.

#### useRecoilValue 와 useSetRecoilValue

```jsx
function TextInput() {
	// const [text,setText] = useRecoilState(textState);
	const text = useRecoilValue(textState);
	const setText = useSetRecoilValue(textState);

	const onChange = (event) => {
		setText(event.target.value);
	};
	...
}
```

위에 있는 것 처럼 get과 set 만을 사용할 수도 있다.

여기 나와있지 않는 `useResetRecoilState`은 atom의 상태를 본래 default값으로 초기화 할 수 있다.

### selector

- recoil에서의 함수 또는 파생된 상태
- 파생된 상태란 atom의 상태에서 파생된 데이터, 즉 atom의 상태에 의존하는 동적인 데이터를 의미
- 주어진 atom의 상태에 대해 항상 동일한 값을 반환하는 순수함수

```jsx
import React from 'react';
import { atom, selector, useRecoilState, useRecoilValue } from 'recoil';

// atom
const countState = atom({
  key: 'countState',
  default: 0,
});

// selector
const doubledCountState = selector({
  key: 'doubledCountState',
  get: ({ get }) => {
    const count = get(countState);
    return count * 2; // countState 값의 두 배를 반환
  },
});

function Counter() {
  const [count, setCount] = useRecoilState(countState);
  const doubledCount = useRecoilValue(doubledCountState);

  const increment = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <h1>Counter</h1>
      <p>Count: {count}</p>
      <p>Doubled Count: {doubledCount}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}

export default Counter;
```

위 결과는 `Increment`를 누르면 `increment` 함수가 실행되어 count + 1을 해준다.
그 후 `doubledCountState` selector가 실행된다. 이 `doubledCountState`는 가까 count + 1이 된 `countState`의 값을 가지고 와서 \*2를 해준 후 return 한다. 그 후 화면에 렌더링 된다.
