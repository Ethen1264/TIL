# 리액트 라우터 돔

### Routing이란 ?

리액트 프로젝트에서 .html 파일의 갯수는 1개이다. 한 개의 웹 페이지 내에서 여러 개의 페이지를 보여주는 방법을 Routing이라고 한다.
-----------------------------------------------
사용자가 요청한 결로에 따라 해당 URL에 맞는 다른 화면을 보여주는 것이다. 리액트에는 이러한 기능이 있지 않기 떄문에 react-router는 라이브러리중 하나이다.

### React-router 설치

#### npm

```javascript 
$ npm install react-router-dom
```

#### yarn

```javascript 
$ yarn add react-router-dom
```
### 사용예시

``` jsx
import React from 'react';
import DayList from './component/DayList';
import Header from './component/Header'
import Day from "./component/Day";
import {BrowserRouter, Routes, Route} from 'react-router-dom';
import EmptyPage from './component/EmptyPage'
import CreateWord from './component/CreateWord';
import CreateDay from './component/CreateDay';


function App() {
  return (
    <BrowserRouter>
      <div className='App'>
        <Header />
        <Routes>
          <Route exact path='/' element={<DayList/>}/>
          <Route path='/day/:day' element={<Day />}/>
          <Route path='/create_word' element={<CreateWord />}/>
          <Route path='/create_day' element={<CreateDay />}/> 
        </Routes>
      </div> 
    </BrowserRouter> 
  );
}

export default App;

```

### 위의 코드 분석하기

#### 1. <BrowserRouter>태그로 컴포넌트 사용하기

- BrowserRouter를 사용 할 것이기 떄문에, <BrowserRouter>태그로 컴포넌트를 감싸야한다.

- Header는 모든 URL에 공통 적용할 Component로 최상단에 위치 할것이다

#### <Routes>, <Route> 컴포넌트 사용하기

- <Routes>컴포넌트는 여러 Route를 감싸서 그 중 규칙이 일치하는 라우트 단 하나만을 렌더링 시켜주는 역할을 한다.
- <Route>는 path속성에 경로, element속성에는 컴포넌트를 넣어 준다. 여러 라우팅을 매칭하고 싶은 경우 URL 뒤에 *을 사용하면 된다.

#### 3. <Link> 컴포넌트 사용하기

- 웹 페이지에서는 원래 링크를 보여줄 때 a태그를 사용한다. 하지만 a태그는 클릭시 페이지를 새로 불러오기때문에 사용하지 않는다.
 - Link 컴포넌트를 사용하는데, 생김새는 a태그를 사용하지만, History API를 통해 브라우저 주소의 경로만 바꾸는 기능이 내장되어 있다.
 - 문법 : <Link to="경로">링크명</Link>
 - import { Link } from 'react-router-dom';
 - <a>와 <Link />의 차이점은 <a>태그는 외부 사이트로 이동하는 경우에 사용, <Link /> 컴포넌트는 프로젝트 내에서 페이지를 전환하는 경우 사용한다.


 ## useNavigate

useNavigate 훅을 실행하면 페이지 이동을 할 수 있게 해주는 함수를 반환한다. <br/>
반환받은 함수의 인자로 설정한 경로를 넘겨주면 해당 경로로 이동할 수 있다. <br/>
Link와 다른 점은 함수 호출을 통해 페이지를 이동하기 때문에 특정 조건을 충족할 경우에 페이지 이동을 하도록 할 수 있다. 

### useNavigate의 형태

```jsx
import { useNavigate } from "react-router-dom";

const navigate = useNavigate();
navigate('경로');
```

### 예시

``` jsx
import { Routes, Route, useNavigate } from "react-router-dom";
import Home from './Home';
import Login from './Login';
import { useState } from 'react';
function App() {
  const [text, setText] = useState('');
  const navigate = useNavigate();

  const goHome = () => {
    setText('Home 페이지')
    navigate('/home');
  }
  const goLogin = () => {
    setText('Login 페이지')
    navigate('/login');
  }
  return (
    <div>
      <p>{text}</p>
      <button type="button" onClick={goHome}>Home</button>
      <button type="button" onClick={goLogin}>Login</button>
      <Routes>
        <Route path="/home" element={<Home />}></Route>
        <Route path="/login" element={<Login />}></Route>
      </Routes>
    </div>
  );
}

export default App;
```

### useParam

```
TIL 15.useParam 페이지를 참고하기 바란다.
```