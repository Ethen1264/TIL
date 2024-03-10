# [#2] RecoilSeletor

### Recoil이 없다면?

React.js는 단방향으로 바인딩을 하는 라이브러리이다. 즉 A와B가 있고 A가 부모 B가 자식이라면 A에서 B로만 props를 사용하여 state를 전달 할 수 있다.

물론 부모의 state를 자식에서 변경 할 순 있지만 효율적이지 않다. 이러한 문제가를 해결하기 위해 Recoil이 등장 했다.

### Redux과 Recoil의 차이

사실 Redux나 Recoil이나 state를 관리한다는 목적은 변함이 없다. 다만 Recoil과 달리 Redux는 리액트 전용으로 만들어진 것이 아니기에 Recoil만큼 React에 적용하는 것이 간단하지 않다. 또한 Redux는 action, reducer, selector, store를 각각 따로 설정하여 복잡한 부분이 있다.

### Selector의 비동기 처리

recoil에서 atom만을 이용해 비동기 처리를 할 수 없다 대신 Seletor만을 이용해서 비동기 처리를 간편하게 할 수 있다.

#### Recoil의 Seletor가 없을 떈

##### atom

```jsx
export const MypagePost = atom({
  key: 'MypagePost',
  default: [],
});
```

##### main

```jsx
import { MypagePost } from '../../recoil'
const [posts, setPosts] = useRecoilState(MypagePost);

useEffect(() => {
  const fetchData = async () => {
    try {
      const response = await instance.get('/user');
      setPosts(response.data.infoPosts);
    } catch (error) {
      console.error('Error fetching data:', error);
    }
  };

  fetchData();
}, []);

{posts.map((posts) => (
          <S.PostBackground key={posts.id}>
            <S.PostContainer>
              <S.ProfileContainer>
                <Profile />
                <S.PostAuthorName>{posts.author}</S.PostAuthorName>
                </S.ProfileContainer>
                </S.PostBackground>
            </S.PostContainer>
           ))}
```

`selector` 없이 `atom`만 이용해서 할수도 있다. 하지만 컴포넌트들이 자동으로 re-render되기 때문에 `selector`가 성능적으로 유리하다.

### Seletor가 있다면

> key : selector를 구분할 수 있는 유일한 id, 즉 key 값을 의미합니다.
>
> get : 에는 derived state 를 return 하는 곳 입니다. 예시 코드에서는 api call을 통해 받아온 data를 return 하게 됩니다. (해당 selector가 갖고 있습니다.)
>
> set : writeable 한 state 값을 변경할 수 있는 함수를 return 하는 곳 입니다.

##### atom

```jsx
export const MypagePost = atom({
  key: 'MypagePost',
  default: [],
});

export const getMypagePost = selector({
  key: 'user',
  get: async ({ get }) => {
    try {
      const { data } = await instance.get('/user');
      return data;
    } catch (e) {
      console.log(e);
    }
  },
  set: ({ set }, data) => {
    set(MypagePost, data);
  },
});
```

##### main

```jsx
import { MypagePost } from '../../recoil'
const [posts, setPosts] = useRecoilState(getMypagePost);

{posts.map((posts) => (
          <S.PostBackground key={posts.id}>
            <S.PostContainer>
              <S.ProfileContainer>
                <Profile />
                <S.PostAuthorName>{posts.author}</S.PostAuthorName>
                </S.ProfileContainer>
                </S.PostBackground>
            </S.PostContainer>
           ))}
```

그렇지만 위와 같이 사용하면 렌더링 할 데이터가 아직 도착하기 이전에 보여줄 fallback UI가 없다는 뜻의 에러메시지가 출력된다.

```jsx
<Suspense fallback={<div>Loading...</div>}>
  <Cookies />
</Suspense>
```
