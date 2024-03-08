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

#### atom

```jsx
const textState = atom({
  key: 'textState',
  default: '',
});
```

`selector`는 `state`를 `get`하여 다른 값으로 변환해 return 해줄 수 있다.

```jsx
const charCountState = selector({
  key: 'charCountState',
  get: ({ get }) => {
    const text = get(textState);

    return text.length;
  },
});
```

```jsx
function CharacterCount() {
	const count = useRecoilValue(charCountState);
	return(
		<>
			<div> Character Count : {count} </div>
		</>
	);
}
```

즉 위에 결과는 selector가 없었다면 `textState`가 나와야 한다. 하지만 selector로 인해 값이 9로 변환되어 9가 출력된다.