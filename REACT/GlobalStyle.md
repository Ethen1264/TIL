# GlobalStyle

CSS에서 기본적으로 초기화 시키는 기본 스타일링을 모아놓는 파일인 것 같았다. 즉 전역 스타일링을 설정하는 것인데 이걸 styled-components로 만들어낸 것을 말한다.


## GlobalStyle 초기 설정

```yarn add styled-components```
그리고 나면 createGlobalStyle이라는 것을 import해서 사용할 수 있다.

#### import하기
import { createGlobalStyle } from 'styled-components';

const GlobalStyles = createGlobalStyle`

## 예시

#### GlobalStyle.jsx

``` jsx
import { createGlobalStyle } from "styled-components";

const GlobalStyle = createGlobalStyle`
body, ul, li {
  padding: 0;
  margin: 0;
  list-style: none;
} 
`;

export default GlobalStyle;
```

#### App.js
``` jsx
import styled from 'styled-components';
import GlobalStyle from './GlobalStyle';
function App() {
  return (
    <> 
    <GlobalStyle/>
      
    </>
  )
}
export default App;
```

이렇게 하면 모든 컴포넌트에 ```padding: 0;``` ```margin: 0;``` ```list-style: none;``` 이렇게 지정할 수 있다.


#### Globalstyle로 폰트 적용법  

```jsx
@font-face {
  font-family: 'Pretendard';
  font-weight: 900;
  font-display: swap;
  src: local('Pretendard Black'),
    url('/fonts/woff2/Pretendard-Black.woff2') format('woff2'),
    url('/fonts/woff/Pretendard-Black.woff') format('woff');
}

@font-face {
  font-family: 'Pretendard';
  font-weight: 800;
  font-display: swap;
  src: local('Pretendard ExtraBold'),
    url('/fonts/woff2/Pretendard-ExtraBold.woff2') format('woff2'),
    url('/fonts/woff/Pretendard-ExtraBold.woff') format('woff');
}

@font-face {
  font-family: 'Pretendard';
  font-weight: 700;
  font-display: swap;
  src: local('Pretendard Bold'),
    url('/fonts/woff2/Pretendard-Bold.woff2') format('woff2'),
    url('/fonts/woff/Pretendard-Bold.woff') format('woff');
}
```

글로벌 스타일에 이런식으로 폰트를 넣어두면 다른 파일에서 스타일드컴포넌트에 폰트의 이름과 속성만 적어도 바로바로 불러와진다.