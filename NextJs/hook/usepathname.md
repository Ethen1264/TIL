# usepathname

현재 url을 확인할 수 있는 훅이다.

```tsx
mport { usePathname } from 'next/navigation';

export default function Navigation() {
  const path = usePathname();
  console.log(path);
  return (
    <nav>
      <ul>
        <li>
          <Link href="/">Home</Link> {path === '/' ? '🔥' : ''}
        </li>
        <li>
          <Link href="/about-us">About Us</Link> {path === '/about-us' ? '🔥' : ''}
        </li>
      </ul>
    </nav>
  );
}
```

usePathname을 이용하여 가지오 온 현제 페이지의 url을 path에 저장을 한다 그후 3항 연산자를 통하여 조건에 따라 출력한다.

