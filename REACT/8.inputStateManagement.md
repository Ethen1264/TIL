# 여러개의 input 상태 관리하기

input 의 개수가 여러개가 됐을때는, 단순히 useState 를 여러번 사용하고 onChange 도 여러개 만들어서 구현 할 수 있지만 좋은 방법은 아니다. 좋은 방법은 더 좋은 방법은, input 에 ```name``` 을 설정하고 이벤트가 발생했을 때 이 값을 참조하는 것이다.

#### inputSample.js

``` JSX
import React, { useState } from 'react';  

function InputSample() {
  const [inputs, setInputs] = useState({
    name: '',
    nickname: ''
  });

  const {name, nickname} = inputs;

  const onChange = (e) => {
    const {value,name} = e.target;
    setInputs({
      ...inputs,
      [name]: value
    });
  };

  const onReset = () => {
    setInputs({
      name: '',
      nickname: '',
    })
  };

  return (
    <div>
      <input name="name" placeholder="이름" onChange={onChange} value={name} />
      <input name="nickname" placeholder="닉네임" onChange={onChange} value={nickname}/>
      <button onClick={onReset}>초기화</button>
      <div>
        <b>값: </b>
        {name} ({nickname})
      </div>
    </div>
  );
}

export default InputSample;
```