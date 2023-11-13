# 첫번째 리액트 컴포넌트 만들기

- src 디렉터리에 Hello.js 라는 파일을 만들어 작성하기 
``` JSX
import React from 'react';

function Hello() {
  return <div>안녕하세요</div>
}

export default Hello;
```
리액트 컴포넌트를 만들 떈 
``` JSX
import React from 'react';
```
를 통해 가지고 와야한다

최하단의 

``` JSX
export default Hello;
```
는 Hello 라는 컴포넌트를 내보내겠다는 의미로 이렇게 해주면 다른 컴포넌트에서 불러와서 사용 할 수 있다.


- 매인 컴포넌트로 돌아가기 (App.js)

``` JSX
import React from 'react';
import Hello from './Hello';


function App() {
  return (
    <div>
      <Hello />
      <Hello />
      <Hello />
    </div>
  );
}

export default App;
```

![](https://i.imgur.com/TraJKdn.png)