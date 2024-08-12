# react-query #3 (useMutation)

### useMutation이란?

PUT, UPDATE, DELETE 와 같이 값을 변경할 때 사용하는 API다.

### useMutation의 용어

> **mutationFn**
> promise 처리가 이루어지는 mutation function
> axios를 이용해 서버에 API를 요청하는 부분
>
> 필수이지만 default mutation 함수가 정의되지 않은 경우에만 해당한다. 비동기 작업을 수행하고 반환하는 함수이며 변순는 mutate 가 mutationFn 에 전달할 객체이다.

> **Mutate**
> useMutation을 이용해 작성한 내용들이 실제로 실행될 수 있도록 돕는 trigger 역할(실제 mutation을 실행하는 함수)을 한다.
> useMutation을 정의해준 후, 이벤트 발생 시 사용한다.

> **onSuccess, onError, onSettled**
> mutation 이 성공했을 때와 실패했을 때 실행되는 함수들 이다. onSettled 의 경우, mutation 이 성공적으로 가져오거나 오류가 발생하여 데이터 또는 오류가 전달될 때 실행된다. 즉, 성공과 실패 두 경우 모두 결과가 전달됩니다.

### 예제 코드

> mutationFn

```tsx
// 첫 번째 방법
const deleteData = useMutation(() => axios.delete(`api/delete/${id}`));

// 두 번째 방법
const deleteData = useMutation({
  mutationFn: (id) => axios.delete(`api/delete/${id}`),
});
```

> mutate

```tsx
const { mutate } = () => deleteData();

const deleteFn = () => {};
```

> onSuccess, onError, onSettled

#### 일반적인 비동기 통신

```tsx
const deleteData = async () => {
  try {
    const res = await axios
      .delete(`api/delete/${id}`)
      .then((res) => console.log(res.data));
  } catch (err) {
    console.error("error", err.message);
  } finally {
    console.log("어쨌든 실행되는 부분");
  }
};
```

#### onSuccess, onError, onSettled 적용

```tsx
// fn key 값 생략된 버전
const deleteData = useMutation((id) => axios.delete(`api/delete/${id}`), {
  onSuccess: () => {
    console.log("요청 성공");
  },
  onError: () => {
    console.error("에러 발생");
  },
  onSettled: () => {
    console.log("결과에 관계 없이 무언가 실행됨");
  },
});

// fn key 값 명시된 버전
const deleteData = useMutation({
  mutationFn: (id) => axios.delete(`api/delete/${id}`),
  onSuccess: () => {
    console.log("요청 성공");
  },
  onError: () => {
    console.error("에러 발생");
  },
  onSettled: () => {
    console.log("결과에 관계 없이 무언가 실행됨");
  },
});
```

### onSuccess의 특징

```tsx
onSuccess: (Reasponse, variable, context) => {
    data...
  },
```

- Reasponse: 서버 통신의 응답
- mutate: 함수의 매계 변수
- context: onMutate()의 return 값
