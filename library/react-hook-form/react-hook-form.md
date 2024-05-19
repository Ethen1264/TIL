# react-hook-form

React Hook Form은 React 기반의 폼 관리 라이브러리로, 폼 상태와 유효성 검사를 처리하기 위한 간편한 방법을 제공합니다. 이를 통해 폼 컴포넌트의 개발과 유지 보수를 용이하게 할 수 있다.

### 패키지 설치

```tsx
npm install react-hook-form
```

### 코드

#### 전체 코드

```tsx
import { useForm } from 'react-hook-form';
import './App.css';
import { useRef } from 'react';

function App() {
  const {
    register,
    watch,
    formState: { errors, isSubmitting, isSubmitted },
    handleSubmit,
  } = useForm();

  const password = useRef();
  password.current = watch('password', '');

  const onSubmit = (data) => {
    console.log('data', data);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <label>Email</label>
      <input
        type="email"
        {...register('email', {
          required: '이메일은 필수 입력입니다.',
          pattern: { value: /^[^@ ]+@[^@ ]+\.[^@ .]{2,}$/, message: '이메일 형식이 맞지 않습니다.' },
        })}
        aria-invalid={isSubmitted ? (errors.email ? 'true' : 'false') : null}
      />
      {errors.email && <p>{errors.email.message}</p>}

      <label>Password</label>
      <input
        type="password"
        {...register('password', {
          required: '비밀번호는 필수 입력입니다.',
          minLength: {
            value: 8,
            message: '8자리 이상의 비밀번호를 사용하세요.',
          },
        })}
      />
      {errors.password && <p>{errors.password.message}</p>}

      <label>Password Confirm</label>
      <input
        type="password"
        {...register('password_confirm', {
          required: '비밀번호 확인은 필수 입력 입니다.',
          validate: (value) => value === password.current || '비밀번호와 일치하지 않습니다',
        })}
      />
      {errors.password_confirm && <p>{errors.password_confirm.message}</p>}

      <input type="submit" disabled={isSubmitting} />
    </form>
  );
}

export default App;
```

#### useForm 설정

```tsx
const {
  register,
  watch,
  formState: { errors, isSubmitting, isSubmitted },
  handleSubmit,
} = useForm();
```

이 부분에서

- register: 폼 필드를 등록하고, 유효성 검사를 설정한다.
- watch: 특정 필드의 값을 실시간으로 감시한다.
- formState: 폼의 상태를 포함한다.
  - errors: 폼의 유효성 검사 오류 정보를 포함한다.
  - isSubmitting: 폼이 제출 중인지 여부를 나타낸다.
  - isSubmitted: 폼이 제출되었는지 여부를 나타낸다.
- handleSubmit: 폼 제출을 처리하는 함수이다.

#### input 설정

```tsx
<input
  type="email"
  {...register('email', {
    required: '이메일은 필수 입력입니다.',
    pattern: { value: /^[^@ ]+@[^@ ]+\.[^@ .]{2,}$/, message: '이메일 형식이 맞지 않습니다.' },
  })}
  aria-invalid={isSubmitted ? (errors.email ? 'true' : 'false') : null}
/>;
{
  errors.email && <p>{errors.email.message}</p>;
}
```

- required: 필수 입력 필드로 설정하며, 검증 실패 시 메시지를 지정한다.
- pattern: 정규식을 사용해 입력값의 형식을 검증하며, 실패 시 메시지를 지정한다.
- aria-invalid: 접근성을 위한 속성으로, 폼이 제출된 후 오류가 있는지 여부를 낸다.
- error: 위의 동작이 실패 했을 때 정의해둔 message를 받아 출력한다.

#### handleSubmit

```tsx
const onSubmit = (data) => {
  console.log('data', data);
};

<form onSubmit={handleSubmit(onSubmit)}>
```

handleSubmit은 함수는 폼 제출 시 호출되는 함수이다.
즉 handleSubmit은이 onSubmit를 폼 제출 시 호출하여 실행한다.
이때 data 매개변수는 폼의 입력값을 포함한다.

```json
{ "email": "test1234@gmail.com", "name": "test", "password": "12345678", "password_confirm": "12345678" }
```

### 이 외의 여러 기능

#### minLength

```tsx
minLength: {
            value: 8,
            message: '8자리 이상의 비밀번호를 사용하세요.',
          },
```

위의 코드와 같이 input의 minLength를 설정할 수 있다.

#### isSubmitting

```tsx
<input type="submit" disabled={isSubmitting} />
```

이 코드와 같이 isSubmitting를 통해 현재 폼이 제출하고 있는지 아닌지 판단하여 폼이 제출 중에 버튼이 다시 눌리는 것을 방지 할 수 있다.
