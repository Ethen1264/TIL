# useEffect란?
컴포넌트가 ```Mount(화면에 첫 렌더링)``` / ```Update(다시 렌더링)``` / ```Unmount(화면에서 사라질떄)``` 특정 작업을 처리할 때 실행시켜주고 싶은 코드를 적으면 된다

### useEffect의 형태

``` JSX
useEffect(() => {
  //작업..
});
```

``` JSX
useEffect(() => {
  //작업..
}, [value]);
```

이렇게 두가지의 종류가 있다. <br/>
첫번째는 렌더링이 될 떄마다 실행된다. <br/>
두번째는 컴포넌트가 맨처음 화면에 렌더링이 될때 실행되거나 value의 값이 바뀔때 실행된다.

### ex)
``` JSX
import React, {useState, useEffect} from 'react';

function App() {
  const [count, setCount] = useState(1);
  const [name,setName] = useState("");

  const handleCountUpdate = () => {
    setCount(count+1);
  };

  useEffect(() => {
    console.log('랜더링 @');
  });

    useEffect(() => {
    console.log('count 변화 %');
  }, [count]);


  useEffect(() => {
    console.log('name 변화 &');
  }, [name]);


  const handleInputChange = (e) => {
    setName(e.target.value);
  };

  return (
    <div>
      <button onClick={handleCountUpdate}>Update</button>
      <span>count: {count} </span>
      <input type="text" value={name} onChange={handleInputChange}/>
      <span>name: {name}</span>
    </div>
  )
}
```