# socket.io를 사용하여 채팅 만들기

### socket.io client 설치

```tsx
npm install socket.io-client
```

### socket function

#### emit

emit은 말을 하는 함수를 뜻한다.

#### on

on은 듣는 함수를 뜻한다.

### socket 생성 (client 웹소켓 세팅)

server.js를 생상하여 io를 불러온 후 소캣 통신을 할 서버의 url를 연결한다.

#### server.js

```tsx
import { io } from 'socket.io-client';
const socket = io('http://localhost:5001');
export default socket;
```

### 사용자 로그인하기

아래의 로직은 `prompt`에 적은 사용자의 이름을 `emit`으로 전송하여 `server`로 전송한다 그후 백엔드에서 받은 `res`를 `useState`에 저장한다. (`res`엔 사용자의 `socket` 토큰과 정보가 담겨져 있다.)

```tsx
const userName = prompt('당신의 이름을 입력하세요');

socket.emit('login', userName, (res) => {
  console.log('Res', res);
  setUser(res.data);
});
```
