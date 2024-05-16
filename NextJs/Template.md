# Template

### Template란?

Template은 레이아웃과 유사하게 자식 레이아웃이나 페이지를 감싸는 역할을 한다. Layout과 다른 점은 탐색할 때, 자식 요소마다 새로운 인스턴스를 생성한다는 것이다.
같은 템플릿을 사용하는 라우트를 이동할 때도 새로운 인스턴스가 마운트되고, DOM 요소가 다시 생성되며 상태가 보존되지 않다. 따라서, Layout과 Template은 공존할 수 없고 둘 중 하나 선택해야 한다.

> 공식 문서에는 템플릿을 사용해야하는 특별한 이유가 없다면, 레이아웃을 사용하는 것이 좋다고 명시되어 있다.

### Template를 쓰는 경우

페이지를 넘나들 때마다 무언가를 기록해야하는 상황에 쓰인다.

### 예시 코드

폴더 안에 template.tsx를 생성 후 아래와 같이 작성하여 활용하면 된다.

```tsx
export default function Template({ children }: { children: React.ReactNode }) {
  return <div>{children}</div>;
}
```
