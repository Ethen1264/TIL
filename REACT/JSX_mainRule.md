# JSX의 기본 규칙 알아보기

- JSX 는 리액트에서 생김새를 정의할 때, 사용하는 문법으로 얼핏보면 HTML 같이 생겼지만 실제로는 JavaScript이다
``` js
return <div>안녕하세요</div>;
```

### 꼭 닫혀야 하는 태그
- 기본 태그는 꼭 닫혀있어야 한다.

![](https://i.imgur.com/gJufFjD.png)

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

- br 같은 태그들도 끝에는 꼭 닫혀야한다.

``` JSX
import React from 'react';
import Hello from './Hello';

function App() {
  return (
    <div>
      <Hello />
      <Hello />
      <Hello />
      <input />
      <br />    //이부분
    </div>
  );
}

export default App;
```

### 꼭 감싸져야하는 태그  

- 두가 이상의 태그는 무조건 하나의 태그로 감싸져있어야 한다.

``` JSX
import React from 'react';
import Hello from './Hello';

function App() {
  return (
    <Hello />
    <div>안녕히계세요.</div>
  );
}

export default App;
```

![](https://i.imgur.com/9kJaJ6i.png)

``` JSX
import React from 'react';
import Hello from './Hello';

function App() {
  return (
    <div>
      <Hello />
      <div>안녕히계세요</div>
    </div>
  );
}

export default App;
```
하지만, 이렇게 단순히 감싸기 위하여 불필요한 div 로 감싸는게 별로 좋지 않은 상황도 있다. 이럴 떈 리액트에서 재공하는 Fragment을 사용하면 된다. (<> </>)

``` JSX
import React from 'react';
import Hello from './Hello';

function App() {
  return (
    <>
      <Hello />
      <div>안녕히계세요</div>
    </>
  );
}

export default App;
```

### JSX 안에 자바스크립트 값 사용하기

JSX 내부에 자바스크립트 변수를 보여줘야 할 때에는 {} 으로 감싸서 보여준다.

``` JSX
import React from 'react';
import Hello from './Hello';

function App() {
  const name = 'react';
  return (
    <>
      <Hello />
      <div>{name}</div> //name 부분에 js 속성 넣기
    </>
  );
}

export default App;
```

### style 과 className
- JSX 에서 태그에 style 과 CSS class 를 설정하는 방법은 HTML 에서 설정하는 방법과 다르다 background-color 처럼 - 로 구분되어 있는 이름들은 backgroundColor 처럼 camelCase 형태로 네이밍 해야한다.
``` JSX
import React from 'react';
import Hello from './Hello';

function App() {
  const name = 'react';
  const style = {
    backgroundColor: 'black',
    color: 'aqua',
    fontSize: 24, // 기본 단위 px
    padding: '1rem' // 다른 단위 사용 시 문자열로 설정
  }

  return (
    <>
      <Hello />
      <div style={style}>{name}</div>
    </>
  );
}

export default App;
```
![](https://i.imgur.com/WN4kTDC.png)

- CSS class 를 설정 할 때에는 class= 가 아닌 className= 으로 설정을 해주어야 한다.

#### App.css
``` css
.gray-box {
  background: gray;
  width: 64px;
  height: 64px;
}
```

#### App.js
``` JSX
import React from 'react';
import Hello from './Hello';
import './App.css';


function App() {
  const name = 'react';
  const style = {
    backgroundColor: 'black',
    color: 'aqua',
    fontSize: 24,
    padding: '1rem'
  }

  return (
    <>
      <Hello />
      <div style={style}>{name}</div>
      <div className="gray-box"></div>
    </>
  );
}

export default App;
```

![](https://i.imgur.com/pEc0VRo.png)

### 주석 

주석은 긴줄을 작성할떈 {/* 이런 형태로 */} 이런 식으로 작성하고
한 줄을 작성할 떈 // 이런 주석을 사용한다

``` JSX
import React from 'react';
import Hello from './Hello';
import './App.css';


function App() {
  const name = 'react';
  const style = {
    backgroundColor: 'black',
    color: 'aqua',
    fontSize: 24, // 기본 단위 px
    padding: '1rem' // 다른 단위 사용 시 문자열로 설정
  }

  return (
    <>
      {/* 주석은 화면에 보이지 않습니다 */}
      <Hello 
      />
      <div style={style}>{name}</div>
      <div className="gray-box"></div>
    </>
  );
}

export default App;
```