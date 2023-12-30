# useMemo란?

### useMemo란?

컴퓨터에서 동일 한 값을 반복적으로 계산 해야할 때 useMemo를 사용하여 계산한 결과의 값을 미리 메모리에 저장해둔다. 이렇게 되면 처음부터 값을 계산하는 게 아닌 메모리에 값을 저장해두어 효율적으로 사용할 수 있다.

이러한 이유는 리액트에서 함수형 컴포넌트가 작동하는 순서에 들어 있다. 리액트는

`렌더링 => 컴포넌트 함수 호출 => 모든 내부 변수 초기화`

이러한 순서를 거치기 떄문이다.

### useMemo를 사용하지 않는다면??

```jsx
function Component() {
  const value = SumNumberChange();
  return <div>{value}</div>;
}

function SumNumberChange() {
  return 10;
}
```

이런식으로 사용하게 되는데 함수를 호출 할 때 마다 value의 값을 초기화하여 효율적이지 않게 사용된다.

### useMemo를 사용하게 된다면??

```jsx
import React, { useMemo } from 'react';

function Component() {
  const value = useMemo(() => {
    return SumNumberChange()
  }, [])
  return <div>{value}</div>;
}

function SumNumberChange() {
  return 10;
}
```

useMemo는 useEffect와 비슷한 형식을 지니고 있는데 첫 번째 인자로 콜백 함수, 두 번째 인자로 의존성 배열(dependancyArray)을 받는다.


