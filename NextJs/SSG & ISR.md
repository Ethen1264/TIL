# & SSG & ISR

### 시작하기 앞서

[ssr & csr](./Rendering.md)

### SSG (Static Site Generation)

서버에서 정적인 사이트를 미리 생성하는 것을 말한다. -> 이는 Next 빌드때 만들어진다.

따라서 서버에서 랜더링 하는 것이 runtime에서 계속 만드는 것이 아닌 1회만 생성된다. (nextjs는 SSG 방식이다.)

#### 장점

- 페이지 로딩 시간이 빠름
- 자바스크립트를 필요로 하지 않음
- SEO에 좋음
- 보안이 뛰어남
- Cached 상태임, 즉 아무리 새로고침을해도 로딩이 없음

#### 단점

- 정적인 내용, pre-rendered된 페이지 이니까
- 실시간 데이터가 아님, pre-rendered다.
- 사용자별 정보 제공이 어려움

### ISR(Incremental Static Regeneration)

서버측에서 주기적으로 HTMl을 서버에서 생성해두고 내려주는걸 말하는데, 처음 빌드 시점에 만들어두고 설정한 주기마다 다시 랜덩리해서 HTML을 생성한다.

#### 장점

- 페이지 로딩 속도가 빠름
- 자바스크립트를 필요로 하지 않는다.
- SEO에 좋음
- 보안이 뛰어남
- Cached 상태
- 데이터가 주기적으로 업데이트가 이루어짐

#### 단점

- 실시간 데이터가 아님
- 사용자별 정보 제공이 어려움

### Hybrid Rendering

NextJS는 Hybrid Web App 이라고도 불리는데, 성능이 좋은 Web App을 만들기 위해 두개 이상의 렌더링 방법을 사용하는걸 의미한다.

예를 들어서 메인 홈페이지는 ISR을 통해서 특정 interval로 업데이트를 하도록 하고,
About Us, QnA와 같이 변경이 거의 이루어 지지 않는 페이지는 SSG로 렌더링을 하고,
사용자의 Profile 페이지는 CSR / SSR을 하이브리드해서 만들 수 있다.

이처럼 하나의 Application에서 페이지의 특성에 따라 적절한 렌더링 방식을 사용해서 만들 수 있고, 심지어는 하나의 페이지 내에서도 하이브리드가 가능하다.

이렇게 처리하면 좋은점은 서버에서 HTML을 미리 생성해서 내려주면 SEO에 유리하고 빠르게 HTML을 응답해줄 수 있다.
그리고 CSR로 처리되는 컴포넌트에 대한 JS만 다운로드가 이루어지기 때문에 사용자는 조금 더 빠르게 Application 이용이 가능해진다.

### SSR과 getServerSideProps()

SSR은 위에서 정리한것처럼, **"페이지에 대한 요청이 있을때마다 서버에서 페이지를 만들어 반환한다."**

A라는 페이지를 서버에서 렌더링하는 SSR방식으로 구현한 페이지로 가정한다면

- 사용자가 A라는 페이지를 초기에 방문했을때도
- 사용자가 B라는 페이지를 갔다가 다시 A라는 페이지로 돌아올때도
- 사용자가 A라는 페이지에 위치해서 새로고침을 눌를때도

계속 서버에 요청하는 것이다.

따라서 Build될때 딱 한번 HTML을 만드는 SSG와 다르게 SSR은 Runtime내내 요청이 있을때마다 서버에서 HTML을 만든다.

### SSR을 언제 쓰는걸까??

User에게 Loading State를 보여주지않고, 한번에 필요한 데이터를 보여주고 싶을 때 사용한다.

```tsx
export default async function SomePage() {
  const response = await fetch("/api/products");
  const data = await response.json();

  return (
    <>
      <span>상품 목록</span>
      <ul>
        {data.map((product) => (
          <li key={product.number}>상품 이름은 {product.name} 입니다.</li>
        ))}
      </ul>
    </>
  );
}
```

GET Request를 이용해서 API한테 전체 상품 목록을 달라고 요청하고, 받아온 전체 상품 목록들을 화면에 뿌려준다고 가정 했을떄

일반적인 CSR로 유저의 브라우저에서 실행이 된다면 아마도 아래와 같은 모습이 된다.

1. 상단에 "상품 목록" 이라는 글자만 보인다. 왜냐면 전체 상품 목록을 아직 불러오고 있기 때문이다.
2. 전체 상품 목록을 다 불러왔다면, 상품의 이름들이 보인다.

여기서 우리는 유저의 입장에서 생각해보면 아래 두가지를 경험하게 된다는걸 알 수 있다.

1. 전체 상품을 아직 다 받아오지 못해도 일부 UI는 먼저 볼 수 있구나?
2. 필요한 데이터 로딩이 완료가 될때까지 나는 로딩이 되는걸 보면서 기다려야 하구나? (Ex. Spinner, 빈화면, 로딩 텍스트 등등등)

이때 `getServerSideProps` 함수로 SSR을 이용하면 유저에게 로딩되는 과정을 보여주지 않고 한번에 필요한 모든데이터를 보여줄 수 있다.

#### getServerSideProps()

```tsx
function SomePage({ data }) {
  return (
    <>
      <span>상품 목록</span>
      <ul>
        {data.map((product) => (
          <li key={product.number}>상품 이름은 {product.name} 입니다.</li>
        ))}
      </ul>
    </>
  );
}

export async function getServerSideProps() {
  const data = await (await fetch("/api/products")).json();

  return {
    props: {
      data,
    },
  };
}

export default SomePage;
```

`getServerSideProps` 함수를 사용하면 서버에서 렌더링할 수 있도록 도와준다.

또한 해당 함수는 클라이언트가 아닌 서버에서 실행되기 때문에 Data Fetch 하거나 DB를 조회할 수 있다.

- 특징

  - getServerSideProps 함수는 서버단에서 Data Fetch나 DB 조회와 같은 기능을 가능하게 한다.
  - getServerSideProps 함수를 사용하면, 해당 함수의 반환값을 화면을 렌더링하는 Component의 입력값으로 자동으로 넣어준다.
  - 결과적으로 서버단에서 필요한 외부데이터를 모두 확보해서 HTML을 모두 렌더링해서 클라이언트한테 넘겨준다.
  - 마지막으로 getServerSideProps 함수는 페이지에 대한 요청이 있을때마다 실행이 된다.

- 단점
  - 페이지의 요청이 있을때 마다 실행되기 때문에 캐싱이 되지 않는다. -> 새로고침을 하면 서버에서 새로 랜더링 해서 HTML을 보내주는 것을 기다려야한다.
  - 유저는 Server에서 랜더링이 완료 될 때 까지 아무것도 볼 수 없다.
    - 가설
      1. 서버에서 어떠한 이유로 느려지게 된다.
      2. 그 결과 pre-rendering 된 HTML을 만드는데 오래 걸린다면
      3. 유저는 HTML이 내려올 때 까지 기달려야한다.
      4. -> 로딩이 오래 걸려서 유저가 어떠한 UI도 못보는 상황은 피하고 싶은데??? 하지만 유저에게 로딩없이 화면은 바로 보여주고싶은걸? 이라는걸 만족하기 위해서 SSG라는게 있다!

### SSG와 getStaticProps, getStaticPaths

getServerSideProps를 활용해서 SSR방식을 사용한다면?

- 서버가 바쁘고 재수가 없으면 서버가 pre-redered된 HTML을 만들때까지 User는 아무런 UI도 보지 못한다.
- 페이지 요청이 있을때마다 HTML을 새로 만들기 때문에 Data가 Cached되지 않고, 서버에 부하를 줄 수 있다.

SSG를 사용하면 이러한 문제를 보완할 수 있다.

SSG는 위에서 이야기 했던 것과 같이 SSG는 Static Site Generation으로 말 그대로 정적인 HTML을 만들어두는걸 이야기한다.
따라서 서버에서 Pre-Rendered 페이지를 방문하면 유저는 어떠한 기다리는 과정없이 바로 페이지를 확인할 수 있다.

이렇게 하면 페이지 요청을 아무리 많이 보내도 서버에서는 추가적인 일을 할 필요없이 그냥 HTML그대로 주면된다, 또한 만들어둔 HTML그대로 쓰기때문에 보여주고자 하는 Data들또한 이미 Cached된 상태다.

#### SSR과 차이점

getServerSideProps + SSR로 만든 페이지를 새로고침하면, 새로고침 할때마다 Server에서 HTML을 만들때까지 기다려야한다.

하지만 SSG로 만들어진 페이지를 아무리 새로고침해봤자 Cached상태 이기 때문에 기다릴 필요가 없다.(SSR보가 훨씬 빠르다.)

#### getStaticProps()

```tsx
function Page({ data }) {
  return (
    <ul>
      {posts.map((post) => (
        <li>{post.title}</li>
      ))}
    </ul>
  );
}

// getStaticProps 함수는 server-side에서 build 타임에만 실행된다.
export async function getStaticProps() {
  // build 타임에 데이터를 받아온다.
  const res = await fetch("/api/products");
  const data = await res.json();

  // { props: { data } }를 반환함으로써,
  // Page 컴포넌트는 빌드타임에 props 로 data 받을 수 있다.
  return {
    props: {
      data,
    },
  };
}

export default Page;
```

getServerSideProps 함수와 크게 다르지 않다

getStaticProps 함수는 Build할때 필요로 하는 외부 데이터를 서버단에서 모두 받아와서 해당 데이터를 포함해서 HTML 페이지를 렌더링한다.
그리고 그 렌더링해둔 HTML페이지를 유저가 요청이 올때마다 전달한다.

이렇게 표시할 화면이 많이 변하지 않는 페이지에 적용하는 것이 좋다.

오케이! 그러면 표시할 화면이 자주 변하는 페이지는?? 그니까 URL이 막 변하는 동적 라우팅은 SSG 어찌 적용해...??

#### getStaticPaths()

SSG가 갖고있는 문제점 중 하나가 바로 동적라우팅을 사용하는 경우다.

여기서 동적라우팅이 뭐냐면 URL이 변하는것들을 의미하는데, URL에 변수가 들어가는 경우라고 생각하면 편하겠다. (Ex: /products/[id])

동적라우팅을 사용해서 query에 들어오는 값들은 NextJS가 빌드할때 알 수 없다.

무슨말이냐!? 위와같이 /products/[id] 에 해당하는 부분을 SSG를 적요하고 싶다고 가정해보자.

그러면 NextJS는 Build할때 모든 데이터가 포함된 HTML을 미리 만들어 두려고 할건데 이렇게 말할거다.

**NextJS: 그래서 HTML을 몇개나 만들어야 하는거야**

즉 NextJS한테 몇개의 HTML을 만들어줘야 하는지 말해줘야 하는데, 이 경우는 Dynamic URL에 대응하는 HTML이기 때문에 `getStaticPaths` 함수를 사용하게 된다.

```tsx
function Post({ post }) {
  // post 렌더링 하는 코드
}

export async function getStaticPaths() {
  // API 호출을 통해 posts 에 대한 데이터를 가져온다.
  const res = await fetch("https://.../posts");
  const posts = await res.json();

  // paths 를 추출한다.
  const paths = posts.map((post) => ({
    params: { id: post.id },
  }));
  /*
	  [{params : {id : 1} }, {params : {id : 2} }]
  */

  return { paths, fallback: false };
}

export async function getStaticProps({ params }) {
  // getStaticProps로부터 params 를 받아 path 를 구성하고 데이터를 받아온다.
  const res = await fetch(`https://.../posts/${params.id}`);
  const post = await res.json();

  return { props: { post } };
}

export default Post;
```

getStaticPaths() 함수로 우리가 만들고자 하는 동적라우팅 페이지들의 Path를 NextJS에게 말해준다. (id:1 / id:2 이런식으로)

그 후 만들고자 하는 Path들의 변수, 즉 /products/[id] 라고 가정하면 [id]에 들어가는 값들을 getStaticPaths()함수가 반환하게 되는거고, 이 반환되는 변수를 getStaticProps() 함수가 인자로 받게된다.

그럼 getStaticProps() 함수는 인자로 받은 변수 [id]를 기반으로, 외부 데이터를 fetch해서 필요한 정보들을 화면을 렌더링하는 컴포넌트에게 props로 넘겨준다.

근데 문제가 있다. 예를 들어서 현재 내 데이터베이스에 등록된 상품의 갯수 약 500만개라고 해보자.

그러면 빌드할때 500만개의 HTML을 미리 만들어둔다...? 이건 미친짓이다.

그럼 어찌해..?

#### option fallback

fallback옵션은 `true` | `fasle` | `"blocking"` 이렇게 3개의 옵션이 있다.

getStaticPaths() 함수를 통해서 미리 만들어진 path가 아닌 다른 path가 URL로 들어오면 어찌해야하나?

404를 반환해줘야 한다고 생각할 수 있지만, 애석하게도 해당 path는 미리 만들어둔 path는 아니지만 분명히 내 DB에 존재하는 path라면...? 아 이럼 404를 띄우면 안된다...

그렇다고 DB에 존재하는 모든 상품을 미리 HTML을 만들어두는건 진짜 미친짓이다, 그리고 새로운 상품이 등록된다면 해당 상품의 페이지도 만들어야 하는데 빌드하는 과정에서 새로운 상품이 들어왔는지 알기는 어렵다.

따라서 미리만둘어두지 않은 path에 대해서도 대응을 해야하고 이럴때 필요한게 바로 getStaticPaths 함수의 fallback 옵션이다.

```tsx
export async function getStaticPaths() {
  return {
    paths: [
      { params: { ... } }
    ],
    fallback: true, false or "blocking"
  };
}
```

위에서 말한것 처럼 fallback옵션은 `true` | `fasle` | `"blocking"` 이렇게 3개의 옵션이 있다.

- false: 404 페이지를 반환한다. 즉 대응하지 않겠다는 소리!
- true: 우선 페이지의 fallback에 해당하는 부분을 보여주고, 뒤에서는 getStaticProps 함수를 통해서 요청을 보내 HTML을 만들라고 시킨다.
  그 이후 HTML이 다 만들어지면 해당 파일은 Pre-Rendered 리스트에 추가하고 화면에 보여준다.
  이후 요청부터는 새로 만드는게 아닌 미리 만들어둔 Pre-Rendered된 HTML을 반환한다.
- "blocking": true와 동작은 유사하나, 파일을 렌더링하는 동안 fallback을 보여주는게 아니라, SSR + getServerSideProps처럼 서버에서 HTML을 다 만들때까지 무작정 기다린다.
  이후 요청부터는 만들어둔 Pre-Rendered된 HTML을 반환한다.

#### fallback

React 18의 Suspnese처럼 서버엣 HTML 파일을 만드는동안 미리 보여줄 화면이다.

```tsx
// pages/posts/[id].js
import { useRouter } from "next/router";

function Post({ post }) {
  const router = useRouter();

  // 만약 페이지가 아직 생성되지 않았다면 getStaticProps()가 실행되는 동안
  // isFallback을 통해 조건을 분기하여 fallback(대체) 페이지를 보여줄 수 있다.
  if (router.isFallback) {
    return <div>Loading...</div>;
  }

  // post 렌더링 하는 코드 생략...
}

export async function getStaticPaths() {
  return {
    // `/posts/1`,`/posts/2`만 빌드타임에 생성된다.
    paths: [{ params: { id: "1" } }, { params: { id: "2" } }],
    // fallback 값을 true로 줌으로써 `/posts/3` 같은 추가 페이지를
    // 정적인 방식으로 생성할 수 있다.
    fallback: true,
  };
}

export async function getStaticProps({ params }) {
  const res = await fetch(`https://.../posts/${params.id}`);
  const post = await res.json();

  return {
    props: { post },
    revalidate: 1,
  };
}

export default Post``;
```

#### SSG와 getStaticProps, getStaticPaths 단점

장점이자 단점인 부분인데 HTML을 딱 1번만 만든다는 점이다.

SSG는 Build할때 HTML을 딱 한번 만들어두고 이를 Pre-Rendered된 HTML이라고 한다.

그렇다면 Build가 다 끝나고난 이후에 바뀐 데이터들은???? 이것들은 HTML에 포함되지 않는다.

따라서 SSG를 사용하면 Latest, Fresh한 Data를 볼 수 없다는게 문제다.

이러한 부분을 `ISR`로 개선할 수 있다.

### ISR (Incremental Static Regeneration)

SSG로 Pre-Redered된 HTML을 최신 데이터로 Update하도록 도와준다.

ISR은 모든 페이지를 다시 빌드할 필요없이, 필요한 페이지만 정적으로 다시 생성한다.

ISR을 이용해서 SSG로 만들어진 HTML을 재생성(업데이트)하는 방법은 크게 2가지다. -> `Revalidate`

#### Revalidate

첫번째 방법은 재생성하는 시간 주기를 설정해주는 방법이다.

이 방법은 getStaticProps() 함수의 옵션인데, 페이지를 방문한 이후로 revalidate 시간 동안은 cached된 페이지를 보여주고 설정한 시간 이후에 들어오는 첫번째 요청에 대해서는 역시 cached된 페이지를 보여주고난 다음에 해당 페이지를 다시 Re-Build한다.

이후에는 역시 새로 만든 HTML을 보여주고, revalidate시간은 다시 흐른다.

revalidate time을 10으로 설정하면, 매 10초마다 HTML을 재생성 하는게 아니라는 것이다.

1~10초까지는 기존의 페이지를 보여주고. 10초가 지난 시점에서 들어오는 첫번째 유저에게는 기존 페이지를 보여주고 바로 페이지를 재생성한다. 그리고 그 다음으로 들어오는 유저에게는 새롭게 만든 페이지를 보여주고 revalidate time의 시계는 다시 움직인다!

```tsx
export async function getStaticProps() {
  const res = await fetch("https://.../posts");
  const posts = await res.json();

  return {
    props: {
      posts,
    },
    // Next.js will attempt to re-generate the page:
    // - When a request comes in
    // - At most once every 10 seconds
    revalidate: 10, // 초 단위
  };
}
```

#### on-demand revalidation

바로 위에서 살펴본 revalidate 옵션을 사용하면, 설정해둔 시간 동안은 cached된 페이지를 보게된다.

그리고 새롭게 재생성 하기 위해서는 설정해둔 시간이 지난 다음에 새로운 요청이 있어야 한다.

반대로 on-demand revalidation은 데이터가 업데이트 될때 Re-Build를 하는 방법이다.

`https://<your-site.com>/api/revalidate?secret=<token>` 을 통해서 NextJS에게 요청을 보내면 되는것으로 보인다.

```tsx
// pages/api/revalidate.js

export default async function handler(req, res) {
  // 토큰 검사
  if (req.query.secret !== process.env.MY_SECRET_TOKEN) {
    return res.status(401).json({ message: "Invalid token" });
  }

  try {
    // 재빌드할 경로명을 정확하게 입력해야한다. req의 body를 통해 받아올 수 있다.
    // 파일명이 "/blog/[slug]" 이더라도 "/blog/post-1" 처럼 입력해야한다.
    await res.revalidate("재빌드할 경로명");
    return res.json({ revalidated: true });
  } catch (err) {
    // 만약 에러가 발생하면 최근에 생성된 페이지를 보여준다.
    return res.status(500).send("Error revalidating");
  }
}
```

#### generateStaticParams()

NextJS 13버전부터 App Route 방식으로 변했다, 그리고 React18을 완벽하게 지원하는데 가장 큰 변화가 바로 `React Server Component`다.

저녀석 때문 더 이상 `getStaticProps`나 `getStaticPaths`, `getServerSideProps`를 안써도 된다.

기존의 NextJS에서는 getServerSideProps 함수 혹은 getStaticProps라는 함수를 이용해서 서버에 접근할 수 있었다.

즉 해당 함수를 사용해서 외부 데이터를 얻어오는 동작을 서버에서 렌더링하면서 할 수 있었다.

때문에, Data fetch등을 수행할때는 반드시 getServerSideProps 또는 getStaticProps 함수를 사용해야 하고, 해당 함수의 반환값을 page를 렌더링하는 컴포넌트의 props로 넘겨서 사용했어야 했다.

반면 React Server Component는 그 자체가 서버에서 렌더링되므로, 컴포넌트 내부에서 Data Fetch를 실행해도 무방하다.

즉, data가 필요한 컴포넌트에서 직접 data fetch가 가능해졌고, NextJS의 App Route의 모든 컴포넌트는 기본적으로 Server Component다.

따라서 더 이상 외부 데이터를 사용하기 위해서 번거로운 행위를 할 필요가 사라졌다.

그냥 해당 컴포넌트에서 async / await을 사용하면 된다.

쉽게 말해서 generateStaticParams는 getStaticProps와 getStaticPaths의 업그레이드 버전이라고 생각하면 된다.

#### getStaticProps를 대체하자

```tsx
export default async function ProductDetail({
  params,
}: {
  params: { id: string };
}) {
  return <span>여기서 props로 받아서 사용하면 개꿀!</span>;
}

export async function generateStaticParams() {
  const products = await PrismaDB.product.findMany({
    select: {
      id: true,
    },
  });

  return products.map((product) => ({
    id: product.id + "",
  }));
}
```

전체적인 사용 방법은 getStaticProps와 차이가 없다.

여기서 주의해야할 부분은 반환 형태는 리스트로 해야하는것과, 렌더링하는 컴포넌트의 함수인자와 동일하게 맞춰서 반환해주는것만 주의해주자.

```
├ ● /products/[id]                       187 B          96.3 kB
├   ├ /products/5
├   ├ /products/6
├   ├ /products/2
├   └ [+2 more paths]
├ ○ /products/add                        22.8 kB         107 kB
├ λ /profile                             160 B          84.5 kB
├ ○ /sms                                 1.43 kB        90.8 kB
└ ○ /test                                448 B          84.8 kB
+ First Load JS shared by all            84.3 kB
  ├ chunks/69-84289ba9e2c20ce0.js        29 kB
  ├ chunks/fd9d1056-5e221561fa023f51.js  53.4 kB
  └ other shared chunks (total)          1.9 kB


ƒ Middleware                             31.4 kB

○  (Static)   prerendered as static content
●  (SSG)      prerendered as static HTML (uses getStaticProps)
λ  (Dynamic)  server-rendered on demand using Node.js
```

저렇게 코드를 작성하고 Build를 해보면 위와 같이 products/[id] 해당 부분에 5개의 pre-rednerd된 페이지가 비르된걸 확인할 수 있다!

#### 그러면 동적URL 대응하는법

그냥 generateStaticParams 함수의 반환값을 빈 리스트를 반환한다.

대신 해당 page.tsx 파일 상단에 `export const dynamicParams = true;`를 선언한다.

```tsx
export const dynamicParams = true;

export default async function ProductDetail({
  params,
}: {
  params: { id: string };
}) {
  return <span>여기서 props로 받아서 사용하면 개꿀!</span>;
}

export async function generateStaticParams() {
  const products = await PrismaDB.product.findMany({
    select: {
      id: true,
    },
  });

  return [];
}
```

위와같이 코드를 작성하면, fallback="blocking"과 같은 형태로 SSG를 구현할 수 있다.

#### ISR을 사용하는법

바로 이전에 Caching 관련 포스팅을 하면서 적어둔 방법을 사용하면 된다.

1. export const revalidate 사용하기

위 예제처럼 10초를 설정해두고 싶다면, page.tsx 상단에 아래와 같이 사용하자.

```tsx
export const revalidate = 10;
```

[revalidate 공식문서](https://nextjs.org/docs/app/api-reference/file-conventions/route-segment-config#dynamic)

2. revalidatePath 사용하기

번거러운 토큰이 아닌 내가 재생성하고 싶은 URL을 함수로 넘겨주면된다.

```tsx
import { revalidatePath } from "next/cache";

revalidatePath("/blog/post-1");
```

[revalidatePath 공식문서](https://nextjs.org/docs/app/api-reference/functions/revalidatePath)
