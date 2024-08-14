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
const askUserName = () => {
  const userName = prompt('당신의 이름을 입력하세요');

  socket.emit('login', userName, (res) => {
    console.log('Res', res);
    setUser(res.data);
  });
};
```

### 메시지 보내기

해당 함수는 input에 넣은 value의 값을 state에 집어 넣고 해당 state를 서버에 전송하는 로직이다.

```tsx
const sendMessage = (event) => {
  event.preventDefault();
  socket.emit('sendMessage', message, (res) => {
    console.log('sendMessage res', res);
  });
};
```

### 메시지 받기

서버에서 온 message를 setMessageList에 저장을 한다.

```tsx
useEffect(() => {
  socket.on('message', (message) => {
    setMessageList((prevState) => prevState.concat(message));
  });
  askUserName();
}, []);
```

### 받은 메시지 화면에 출력하기

서버에서 넘겨준 메시지의 유저 정보와 현재 사용자의 유저 정보를 비교하여 조건에 따라 랜더링 한다.

```tsx
const MessageContainer = ({ messageList, user }) => {
  return (
    <div>
      {messageList.map((message, index) => {
        return (
          <Container key={message._id}>{message.user.name === user.name ? <div>...</div> : <div>...</div>}</Container>
        );
      })}
    </div>
  );
};

export default MessageContainer;
```

### 채팅방 정보 받아오기

```tsx
const [rooms, setRooms] = useState([]);

useEffect(() => {
  socket.on('rooms', (res) => {
    setRooms(res);
  });
}, []);
```

### 채팅방 정보 화면에 출력하기

```tsx
import React from 'react';
import { useNavigate } from 'react-router-dom';
import './RoomListPageStyle.css';

const RoomListPage = ({ rooms }) => {
  const navigate = useNavigate();

  const moveToChat = (rid) => {
    navigate(`/room/${rid}`);
  };

  return (
    <div className="room-body">
      <div className="room-nav">채팅 ▼</div>

      {rooms.length > 0
        ? rooms.map((room) => (
            <div key={room._id} onClick={() => moveToChat(room._id)}>
              <div>
                <img src="/profile.jpeg" alt="Profile" />
                <p>{room.room}</p>
              </div>
              <div>{room.members.length}</div>
            </div>
          ))
        : null}
    </div>
  );
};

export default RoomListPage;
```

### 채팅방 나가기

```tsx
const leaveRoom = () => {
  socket.emit('leaveRoom', user, (res) => {
    if (res.ok) navigate('/');
  });
};

<nav>
  <Button onClick={leaveRoom}>←</Button>
  <div>{user.name}</div>
</nav>;
```
