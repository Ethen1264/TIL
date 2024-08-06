# infinite scroll

### 무한스크롤의 원리

![alt text](./img/infinite-scroll.png)

#### 콘텐츠 영역

우선 콘텐츠 영역에 몇 개의 콘텐츠를 보여줄 것인지 정하는 게 중요하다.
백엔드 파트에서 보내줄 응답 데이터를 가공할 때, 한 페이지 당 몇 개의 콘텐츠까지 보여줄 것인지 코드를 작성해야하기 때문이다.
그리고 첫 페이지 API를 불러와 본인의 콘텐츠 영역에 나타내주면 되고, 개수에 따라 자연스레 스크롤이 생성될 것이다.

#### API 호출 영역

해당 부분은 보여주는 데이터의 개수가 끝났을 때, 다음 페이지에 대한 API를 호출하기 위한 호출 영역이다.
보통은 콘텐츠 영역의 스크롤이 끝날 때 쯔음 해당 영역이 나타나게 된다.

### 무한스크롤 문법

- pageParam

  페이지 값을 매개변수로 넘겨서 API를 호출할 때, 페이지 매개변수를 포함하는 배열이다.

- initialPageParam

initialPageParam은 초기 페이지 시작을 몇 부터 할 것인지 정할 수 있다.

```tsx
initialPageParam: 1;
```

- getNextPageParam

로드해야 할 데이터가 있는지의 여부 판단과 어떤 동작을 할 것인지를 작성하는 옵션이다.

- isLoading

API를 호출 후 모두 완료되었는지 판단하는 boolean 객체다.

- hasNextPage

pageParam을 더 늘려 불러올 데이터가 있는지 판단하는 boolean 객체다.

- fetchNextPage

이는 다음 페이지용 API 호출 영역에서 사용하게 될텐데,
호출 영역을 만나게 되면 getNextPageParam로 정의한 코드를 실행시킬 수 있도록 fetchNextParam을 불러와 실행시키는 용도다.

### useInfiniteQuery 활용법 예제 코드

```tsx
import { useEffect } from "react";
import TodoCard from "./components/TodoCard";
import { todo } from "./types/todo";
import "./App.css";
import { useInView } from "react-intersection-observer";
import { useInfiniteQuery } from "@tanstack/react-query";

function App() {
  const { ref, inView } = useInView();

  const fetchTodos = async ({ pageParam }: { pageParam: number }) => {
    const res = await fetch(
      `https://jsonplaceholder.typicode.com/todos?_page=${pageParam}`
    );
    return res.json();
  };

  const {
    data,
    status,
    error,
    fetchNextPage,
    isFetchingNextPage,
    hasNextPage,
  } = useInfiniteQuery({
    queryKey: ["todos"],
    queryFn: fetchTodos,
    initialPageParam: 1,
    getNextPageParam: (lastPage, allPages) => {
      // lastPage는 최근에 가져온 페이지의 데이터, allPages는 지금까지 가져온 모든 페이지의 데이터
      const nextPage = lastPage.length ? allPages.length + 1 : undefined;
      return nextPage;
    },
  });

  const content = data?.pages.map((todos: todo[]) =>
    todos.map((todo) => {
      return <TodoCard innerRef={ref} key={todo.id} todo={todo} />;
    })
  );

  useEffect(() => {
    if (inView && hasNextPage) {
      fetchNextPage();
    }
  }, [inView]);

  if (status === "pending") return <p>loading...</p>;

  if (status === "error") return <p>Error: {error.message}</p>;

  return (
    <div className="app">
      {content} {isFetchingNextPage && <h3>Loading...</h3>}
    </div>
  );
}

export default App;
```

### 무한 스크롤 지점 확인하기

돔의 상태를 확인할 수 있는 라이브러리인 `react-intersection-observer`를 사용했다.

```tsx
npm install react-intersection-observer
```

```tsx
const { ref, inView } = useInView();
```

이렇게 선언을 한다.

- ref

  - ref는 감지할 DOM 요소에 연결하기 위해 사용되는 참조한다.
  - ref를 특정 요소에 연결하면, 그 요소가 화면에 들어올 때 또는 화면에서 나갈 때 이를 감지할 수 있다.

- inView
  - inView는 boolean 값으로, 참조된 요소가 현재 화면에 보이는지 여부를 나타낸다.
  - 요소가 화면에 들어오면 inView는 true가 되고, 화면에서 나가면 false가 된다.

```tsx
useEffect(() => {
  if (inView && hasNextPage) {
    fetchNextPage();
  }
}, [inView]);
```

즉 위의 코드와 같이 useEffect에서 inView가 true가 될 때마다 fetchNextPage()를 호출하여 새로운 데이터를 가져온다.
