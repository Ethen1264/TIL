# What are Server Actions?

React Server Action은 비동기 코드를 서버에서 직접 실행할 수 있게 해준다. Server Action은 여러 공격을 방어하고, 데이터를 안전하게하고, 허가된 접근을 보장하기 위해 효율적인 보안 솔루션을 제공한다.

### Next.js with Server Actions

Server Action은 Next.js의 캐싱과도 깊게 연관되어있다. form이 Server Action을 통해 제출되었을 때, data를 변경하는 뿐만아니라, revalidatePath 와 revalidateTag 와 같은 API들을 이용하는 것으로 연관된 캐시들을 다시 업데이트 할 수 있다.

### Server Action을 만드는 방법

```
'use server';
```

본인이 server action을 사용할 부분의 최상단에 추가한다.

```tsx
// Server Component
export default function Page() {
  // Action
  async function submit(formData: FormData) {
    'use server';

    const response = await fetch('url', {
      method: 'post',
      body: data
    };)
  }

  // Invoke the action using the "action" attribute
  return <form action={submit}>...</form>;
}
```
