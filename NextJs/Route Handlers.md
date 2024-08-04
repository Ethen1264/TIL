# Route Handlers

### Route Handlers란?

루트 핸들러는 웹의 요청/응답 API들을 이용하여 특정 루트에 커스텀 리퀘스트 핸들러를 생성할 수 있도록 도와준다.

### Convention

루트 핸들러는 app디렉토리 내의 route.js | ts파일에 정의한다.

```tsx
// app/api/route.ts

export async function GET(request: Request) {}
```

루트 핸들러는 page.js나 layout.js와 비슷하게 app 디렉토리 내에 중첩될 수 있다. 하지만 page.js와 같은 루트 세그먼트 레벨에는 route.js파일이 올 수 없다.

### 지원되는 HTTP 메서드

`GET`, `POST`, `PATCH`, `DELETE`, `HEAD`, `OPTIONS` 이외 지원되지 않는 메서드를 호출하면 `GET, POST, PATCH, DELETE, HEAD, 그리고 OPTIONS`가 response된다.

### 라우트 핸들러의 필요성

1. 통합된 경로 관리: route.js 파일을 사용하여 각 경로에 대한 로직을 중앙에서 관리할 수 있으며, API 라우트처럼 HTTP 메서드(GET, POST 등)를 직접 처리할 수 있습니다.
2. 성능 최적화: 캐싱과 같은 기능을 이용하여 네트워크 요청의 부하를 줄이고, 응답 속도를 개선할 수 있습니다.
3. 보안 강화: 입력 검증, 인증과 같은 보안 관련 처리를 라우트 핸들러에서 수행함으로써 보안을 강화할 수 있습니다.
4. 유연한 응답 구성: 다양한 HTTP 상태 코드와 헤더를 설정하여, 요청에 따른 정교한 응답을 구성할 수 있습니다.

### 라우트 헨들러를 사용하는 경우

사용자의 로그인 요청을 처리하거나, 데이터베이스에서 정보를 조회하여 반환하는 API, 파일 업로드 처리 등 복잡한 로직을 구현할 때 유용하다. 또한, 동적인 웹 페이지에서 클라이언트의 요청에 따라 콘텐츠를 즉각적으로 업데이트하는 등의 인터랙티브한 기능 구현에 필수적이다.

이처럼 라우트 핸들러는 Next.js 애플리케이션에서 백엔드 로직을 효율적으로 관리하고 최적화할 수 있는 중요한 기능으로 자리잡고 있다. 이를 통해 개발자는 더욱 빠르고 안전하며 유연한 웹 애플리케이션을 구축할 수 있다.

### 라우트 핸들러 설정하기

```tsx
// 데이터 조회
export async function GET(request) {
  return new Response(JSON.stringify({ message: '데이터 조회' }), {
    headers: { 'Content-Type': 'application/json' },
  });
}

// 데이터 생성
export async function POST(request) {
  return new Response(JSON.stringify({ message: '데이터 생성' }), {
    headers: { 'Content-Type': 'application/json' },
  });
}

// 데이터 수정
export async function PUT(request) {
  return new Response(JSON.stringify({ message: '데이터 수정' }), {
    headers: { 'Content-Type': 'application/json' },
  });
}

// 데이터 삭제
export async function DELETE(request) {
  return new Response(JSON.stringify({ message: '데이터 삭제' }), {
    headers: { 'Content-Type': 'application/json' },
  });
}
```

이렇게 구성된 라우트 핸들러를 통해 개발자는 요청된 HTTP 메서드에 따라 적절한 응답을 할 수 있으며, 복잡한 애플리케이션 로직을 효과적으로 관리할 수 있다. 이를 통해 사용자의 경험을 개선하고, 애플리케이션의 성능을 최적화할 수 있는 기회를 제공한다.

### NextRequest 및 NextResponse의 확장 기능

NextRequest 객체는 요청과 관련된 다양한 메타데이터에 접근할 수 있게 해주며, NextResponse 객체는 응답을 더욱 세밀하게 제어할 수 있는 메서드들을 제공한다.

```tsx
import { NextRequest, NextResponse } from 'next/server';

export function middleware(request: NextRequest) {
  const response = NextResponse.next();
  // 요청 처리 로직
  return response;
}
```

### 쿠키와 헤더 다루기

#### 쿠키 설정 및 접근

```tsx
export function handler(req, res) {
  // 쿠키 설정
  res.cookie('session_id', '123456', { secure: true, httpOnly: true });
  // 쿠키 접근
  const sessionId = req.cookies['session_id'];
  return res.json({ sessionId });
}
```

#### 헤더 설정 및 읽기

```tsx
export function handler(req, res) {
  // 요청 헤더 읽기
  const userAgent = req.headers['user-agent'];

  // 응답 헤더 설정
  res.setHeader('Custom-Header', 'value');
  return res.json({ userAgent });
}
```

### 캐싱과 최적화

Next.js에서 GET 메서드를 사용할 때의 기본 캐싱 동작은 응답 효율성을 높이기 위해 중요하다. 서버가 동일한 요청에 대해 반복적으로 같은 계산을 수행하는 것을 방지함으로써 더 빠른 로드 시간과 낮은 서버 부하를 제공한다.

```tsx
export async function GET() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();
  return new Response(JSON.stringify(data), { status: 200 });
}
```

### 캐싱에서 제외되는 시나리오와 동적 기능 사용

1. 동적 데이터 처리: 요청마다 다른 결과를 반환해야 하는 API는 캐시에서 제외된다.
2. 사용자 인증 데이터: 로그인한 사용자의 정보나 세션 데이터 같은 인증 관련 정보는 보안상의 이유로 캐시되지 않다.
3. HTTP 메서드 사용: POST, PUT, DELETE 같은 수정이 이루어지는 HTTP 메서드는 캐싱이 적용되지 않다.

[참고 자료](https://reactnext-central.xyz/blog/nextjs/route-handlers)
