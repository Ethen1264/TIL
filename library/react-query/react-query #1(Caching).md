# react-query #1(Caching)

## react-query란?

- 공식문서의 정의

> fetching, caching, 서버 데이터와의 동기화를 지원해주는 라이브러리

React-Query는 프론트엔드에서 비동기 데이터를 불러오는 과정 중 발생하는 문제들을 해결해준다.

### 캐싱

캐싱은 동일한 데이터에 대한 반복적인 비동기 데이터 호출을 방지하고, 이는 불필요한 API 콜을 줄여 서버의 부하를 줄이는 것을 말한다.

그렇다면 react-query는 데이터의 변경을 어떻게 인식하는 것 일까?

### react-query의 데이터 갱신 방법

리액트 쿼리는 아래와 같은 경우 재갱신을 시도한다.

```
1. 화면을 보고 있을 때
2. 페이지의 전환이 일어났을 때
3. 페이지 전환 없이 이벤트가 발생해 데이터를 요청할 때
```

이러한 설정은 react-query에서 제공하고 있는데 아래와 같이 설정할 수 있다.

```
refetchOnWindowFocus, //default: true
refetchOnMount, //default: true
refetchOnReconnect, //default: true
staleTime, //default: 0
cacheTime, //default: 5분 (60 * 5 * 1000)
```

### react-query의 용어

- refetchOnWindowFocus : 브라우저에 포커스가 들어온 경우
- refetchOnMount : 새로운 컴포넌트 마운트가 발생한 경우
- refetchOnReconnect : 네트워크 재연결이 발생한 경우

#### staleTime & cacheTime

##### staleTime

- staleTime은 데이터가 fresh에서 stale 상태로 변경되는 데 걸리는 시간이다.
- fresh 상태일 때는 Refetch 트리거(위의 3가지 경우)가 발생해도 Refetch가 일어나지 않는다
- 설정해주지 않는다면 Refetch 트리거가 발생했을 때 바로 Refetch가 발생한다.

##### cacheTime

- cacheTime은 데이터가 inactive한 상태일 때 캐싱된 상태로 남아있는 시간이다.
- 특정 컴포넌트가 unmount 되면 사용된 데이터는 inactive상태로 바뀌고, 이때 데이터는 cacheTime만큼 유지된다.
- cacheTime 이후 데이터는 가비지 콜렉터로 수집되어 메모리에서 해제된다.
- 만일 cacheTime이 지나지 않았는데 해당 데이터를 사용하는 컴포넌트가 다시 mount되면, 새로운 데이터를 fetch해오는 동안 캐싱된 데이터를 보여준다.
- 즉, 캐싱된 데이터를 계속 보여주는게 아니라 fetch하는 동안 임시로 보여준다.
