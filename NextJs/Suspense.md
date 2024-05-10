# Suspense

### Suspense란?

<Suspense>는 React에서 무언가를 기다릴 때 한다. 이때 children이 로딩되기 전에 fallback을 보여줄 수 있다.

### Suspense를 적용하면?

```tsx
MovieInfo.tsx;

import { API_URL } from '@/app/(home)/page';

async function getMovie(id: string) {
  console.log(`Fetching movies: ${Date.now()}`);
  await new Promise((resolve) => setTimeout(resolve, 5000));
  const response = await fetch(`${API_URL}/${id}`);
  return response.json();
}

export default async function MovieInfo({ id }: { id: string }) {
  const movie = await getMovie(id);
  return <h6>{JSON.stringify(movie)}</h6>;
}
```

```tsx
MovieVideos.tsx;

import { API_URL } from '@/app/(home)/page';

async function getVideos(id: string) {
  console.log(`Fetching videos: ${Date.now()}`);
  await new Promise((resolve) => setTimeout(resolve, 3000));
  const response = await fetch(`${API_URL}/${id}/videos`);
  return response.json();
}

export default async function MovieVideos({ id }: { id: string }) {
  const videos = await getVideos(id);
  return <h6>{JSON.stringify(videos)}</h6>;
}
```

```tsx
MovieDetail.tsx;

export default async function MovieDetail({ params: { id } }: { params: { id: string } }) {
  return (
    <div>
      <Suspense fallback={<h1>Loading movie info</h1>}>
        <MovieInfo id={id} />
      </Suspense>
      <Suspense fallback={<h1>Loading movie videos</h1>}>
        <MovieVideos id={id} />
      </Suspense>
    </div>
  );
}
```

이렇게 서버와 통신하는 두 컴포넌트를 임포트 하여 `Suspense`라는 컴포넌트로 각각 감싼다. 이때 `fallback`을 사용하여 통신이 끝나기 전까지의 상태를 출력할 수 있다. 또한 Suspense로 감쌀 시 기존 처럼 `MovieVideos`의 통신이 끝나고 `MovieInfo`의 통신이 끝날 때 까지 기다렸다가 화면에 두개를 같이 렌더링 하는 것이 아닌 각각 통신이 끝나자마자 화면에 랜더링 할 수 있다.
