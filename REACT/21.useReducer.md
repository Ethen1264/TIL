# useReducer 

### Reducer의 함수
1. state
 - 컴포넌트에서 사용할 상태
2. dispatch 함수
 - 첫번째 인자인 reducer 함수를 실행시킨다.
 - 컴포넌트 내에서 state의 업데이트를 일으키키 위해 사용하는 함수
3. reducer 함수
 - 컴포넌트 외부에서 state를 업데이트 하는 함수
 - 현재state, action 객체를 인자로 받아, 기존의 state를 대체하여 새로운 state를 반환하는 함수
4. initialState
 - 초기 state
5. init
 - 초기 함수 (초기 state를 조금 지연해서 생성하기 위해 사용)


### useReducer 이해하기

예전엔 상태를 업데이트 할 때에는 `useState` 를 사용해서 새로운 상태를 설정해주었는데 다른 방법으론 `useReducer`가 있다. 이 Hook 함수를 사용하면 컴포넌트의 상태 업데이트 로직을 컴포넌트에서 분리시킬 수 있다. 상태 업데이트 로직을 컴포넌트 바깥에 작성 할 수도 있고, 심지어 다른 파일에 작성 후 불러와서 사용 할 수도 있다.


### useState로 만드 카운터 

``` jsx
import React, { useState } from 'react';

function Counter() {
  const [number, setNumber] = useState(0);

  const onIncrease = () => {
    setNumber(prevNumber => prevNumber + 1);
  };

  const onDecrease = () => {
    setNumber(prevNumber => prevNumber - 1);
  };

  return (
    <div>
      <h1>{number}</h1>
      <button onClick={onIncrease}>+1</button>
      <button onClick={onDecrease}>-1</button>
    </div>
  );
}

export default Counter;
```

`useReducer` Hook 함수를 사용해보기전에 우선 `reducer` 가 무엇인지 알아야 한다. `reducer` 는 현재 상태와 액션 객체를 파라미터로 받아와서 새로운 상태를 반환해주는 함수이다.

```jsx
function reducer(state, action) {
  // 새로운 상태를 만드는 로직
  // const nextState = ...
  return nextState;
}
```

`reducer` 에서 반환하는 상태는 곧 컴포넌트가 지닐 새로운 상태가 된다.
여기서 `action` 은 업데이트를 위한 정보를 가지고 있다. (주로 `type` 값을 지닌 객체를 사용하지만 지키지 않아도 된다.)

그렇다면 `action`의 예시론 

``` jsx
// 카운터에 1을 더하는 액션
{
  type: 'INCREMENT'
}
// 카운터에 1을 빼는 액션
{
  type: 'DECREMENT'
}
// input 값을 바꾸는 액션
{
  type: 'CHANGE_INPUT',
  key: 'email',
  value: 'tester@react.com'
}
// 새 할 일을 등록하는 액션
{
  type: 'ADD_TODO',
  todo: {
    id: 1,
    text: 'useReducer 배우기',
    done: false,
  }
}
```

`useReducer` 의 사용법은 

``` jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

여기서 `state` 는 우리가 앞으로 컴포넌트에서 사용 할 수 있는 상태를 가르키게 되고, `dispatch` 는 액션을 발생시키는 함수이다. 이 함수는 다음과 같이 사용된다. `dispatch({ type: 'INCREMENT' })`.

그리고 `useReducer` 에 넣는 첫번째 파라미터는 `reducer` 함수이고, 두번째 파라미터는 초기 상태이다

이제 위에 useState로 만든 counter를 useReducer로 바꾸면

#### Counter

```jsx
import React, { useReducer } from 'react';

function reducer(state, action) {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state - 1;
    default:
      return state;
  }
}

function Counter() {
  const [number, dispatch] = useReducer(reducer, 0);

  const onIncrease = () => {
    dispatch({ type: 'INCREMENT' });
  };

  const onDecrease = () => {
    dispatch({ type: 'DECREMENT' });
  };

  return (
    <div>
      <h1>{number}</h1>
      <button onClick={onIncrease}>+1</button>
      <button onClick={onDecrease}>-1</button>
    </div>
  );
}

export default Counter;
```