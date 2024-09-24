# What are Server Actions?

React Server Action은 비동기 코드를 서버에서 직접 실행할 수 있게 해준다. Server Action은 여러 공격을 방어하고, 데이터를 안전하게하고, 허가된 접근을 보장하기 위해 효율적인 보안 솔루션을 제공한다.

### Next.js with Server Actions

Server Action은 Next.js의 캐싱과도 깊게 연관되어있다. form이 Server Action을 통해 제출되었을 때, data를 변경하는 뿐만아니라, revalidatePath 와 revalidateTag 와 같은 API들을 이용하는 것으로 연관된 캐시들을 다시 업데이트 할 수 있다.

### 장점

- SEO 향상: SSR(Server-Side Rendering)을 통해 페이지 로딩 속도를 높여 검색 엔진 최적화(SEO)에 도움이 된다.
- 더 나은 사용자 경험: 페이지 로딩 시점에 데이터를 미리 준비하여 클라이언트 측 렌더링보다 더 부드러운 사용자 경험을 제공한다.
- 보안 강화: 클라이언트 측에서 민감한 데이터를 노출하지 않고 서버 측에서 처리하여 보안을 강화할 수 있다.
- 서버 측 유효성 검증: 입력 데이터 유효성 검증을 서버 측에서 수행하여 클라이언트 측 공격을 방지할 수 있다.
- 다양한 라이브러리 지원: 서버 측에서 Node.js 환경을 활용하여 다양한 라이브러리를 사용할 수 있다.

### 단점

- 복잡성 증가: 서버 측 코드를 추가해야 하기 때문에 개발 및 유지 관리가 더 복잡해질 수 있습니다.
- 서버 부하 증가: 서버 측에서 더 많은 작업을 수행하기 때문에 서버 부하가 증가하고 비용이 발생할 수 있습니다.
- 클라이언트 측 기능 제한: 클라이언트 측에서만 작동하는 라이브러리 또는 기능은 사용할 수 없습니다.
- 디버깅 어려움: 서버 측 코드는 클라이언트 측 코드보다 디버깅이 더 어려울 수 있습니다.

### Server Action을 만드는 방법

server action을 사용할땐 여러 조건이 필요하다.

1. "use server" keyword는 server action 함수 최상단에 작성한다.
2. server action 함수는 button의 onClick 이벤트가 아닌, form의 action 이벤트에 할당한다.

```tsx
<form action={formAction}>
```

3. form에서 사용하는 input 엘리먼트는 모두 name을 넣어줘야한다.

```tsx
<input type="email" name="email" required />
```

```tsx
// app/login/page.tsx
"use client";

import { useFormState } from "react-dom";

// 서버 액션 정의
async function loginAction(prevState: any, formData: FormData) {
  "use server";

  const email = formData.get("email") as string;
  const password = formData.get("password") as string;

  // 간단한 인증 로직 (실제 구현에서는 더 안전한 방식 사용 필요)
  if (email === "user@example.com" && password === "password") {
    // 로그인 성공 시 처리
    // 예: 세션 설정, 데이터베이스 업데이트 등
    return { success: true };
  } else {
    return { success: false };
  }
}

export default function LoginPage() {
  const [state, formAction] = useFormState(loginAction, { success: false });

  return (
    <form action={formAction}>
      <input type="email" name="email" required />
      <input type="password" name="password" required />
      <button type="submit">로그인</button>
      {state.success && <p>로그인 성공!</p>}
    </form>
  );
}
```
