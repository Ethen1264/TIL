# 리액트를 yarn을 이용해 실행하기

- 시작에 앞서 새로운 프로잭트를 생성하고 터미널을 열기 
- 다음 코드를 작성하기
``` 
  $ npx create-react-app begin-react 
```
- 그 yarn을 실행하기 
``` 
  $ cd begin-react
  $ yarn start  
```

만약 module not found: error: can't resolve 'styled-components' 오류가 생기면
styled-components 라이브러리를 설치 해야한다
```
  $ yarn add styled-components
```