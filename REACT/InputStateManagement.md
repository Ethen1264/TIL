# input 상태 관리하기

#### InputSample.js
``` JSX
import React from 'react' ;

function InputSample() {
  return (
    <div>
      <input />
      <button>초기화</button>
      <div>
        <b>값: </b>
      </div>
    </div>
  )
}
```

#### App.js
``` JSX
import React from 'react';
import InputSample from './inputSample';

function App() {
  return (
    <InputSample />
  );
}

export default App;
```

input 에 입력하는 값이 하단에 나타나게 하고, 초기화 버튼을 누르면 input 이 값이 비워지도록 구현을 하기 위해선 ```useState```를 사용해야 한다.

#### inputSample.js

``` JSX
import React, { useState } from 'react';

function InputSample() {
  const [text, setText] = useState('');

  const onChange = (e) => {
    setText(e.target.value);
  };

  const onReset = () => {
    setText('');
  };

  return (
    <div>
      <input onChange={onChange} value={text}  />
      <button onClick={onReset}>초기화</button>
      <div>
        <b>값: {text}</b>
      </div>
    </div>
  );
}

export default InputSample;
```