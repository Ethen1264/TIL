# react-query #2 (useQuery)

## useQuery란?

> http 메서트가 get인 api통신을 캐싱 할 때 사용한다.

### QueryClient

```tsx
import {
  QueryClient,
  QueryClientProvider,
} from '@tanstack/react-query'

const queryClient = new QueryClient()

export default function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <Example />
    </QueryClientProvider>
  )
```

위에 보이는 것과 같이 컴포넌트의 최상단 컴포넌트에 QueryClientProvider 컴포넌트를 감싸주고 client 에 생성한 queryClient 객체를 props 로 전달한다.

### useQuery

#### useQuery의 기본 형태

```tsx
useQuery(쿼리 키, 쿼리 함수, 옵션)
```

useQuery 에는 3개의 인자를 전달 할 수 있고 첫번째 자리는 쿼리키를 두번째 자리는 쿼리함수를 세번째 자리는 옵션을 전달 한다.

#### Query Key

유니크한 쿼리 키는 다른 곳에서도 동일한 쿼리를 불러올 때 유용하게 사용된다. 유니크한 쿼리 키는 리액트 쿼리가 쿼리 데이터를 판별하는 데 사용된다.

#### Query Function

useQuery를 통해서 쿼리를 정의할 때 전달하는 함수이다. 비동기 익명 함수, 정의해둔 함수를 전달할 수 있다.

#### useQuery의 반환값

- status : 비동기 로직의 현재 상태를 반환합니다. idle 이 초기 상이다.
- loading : 데이터를 요청 중인 상태이다.
- error : 데이터 요청이 실패한 상태이다.
- succerss : 데이터 요청에 성공한 상태이다.
- isLoading : 로딩중인지 여부를 나타낸다.
- isFetching : 리액트 쿼리가 요청 중인지 여부를 나타낸다.
- inSucess : 요청 성공 여부를 나타냅다.
- inError : 요청 실패로 에러 여부를 나타냅다.
- data : 서버로부터 요청하여 받은 데이터이다.
- error : 요청 실패에 대한 에러 내용이다.
- refetch : 수동적으로 서버에게 데이터 요청을 할 수 있습니다. 이때는 리액트 쿼리가 모든 옵션을 무시하고 무조건 서버에 데이터 요청한다.

#### 예시

```tsx
function Example() {
  const { isLoading: isDataLoading, error, data:responseData } = useQuery({
    'responseData'
    queryFn: () =>
      fetch('https://react-queryTest').then(
        (res) => res.json(),
      ),
  })

  if (isDataLoading) return 'Loading...'

  if (error) return 'error' + error.message

  return (
    <div>
      <h1>{responseData.name}</h1>
      <p>{responseData.description}</p>
      <p>{responseData.number}</p>
    </div>
  )
}
```

useQuery 함수가 반환하는 객체를 보면 isDataLoading 을 통해 로딩 여부를, error 를 통해 에러 발생 여부를, data를 통해 성공 시 데이터를 반환할 수 있다.

(종종 api통신을 진행을 해서 response된 값을 변수나 useState에 넣어주는데 이 코드에선 response된 값을 어떻게 저장을 하는지 의문을 가질수도 있다. useQuery에선 위에서 정의한 data에 값이 들어간다.)
