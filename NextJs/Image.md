# Image

### nextjs가 Image를 권장하는 이유

> next.js에서는 <img /> 태그 사용보다는 next에서 제공하는 <Image /> 컴포넌트 사용을 권장하고 있다. <img /> 태그의 ighthouse로 성능을 확인해 본 결과 Performance 부분에서 70점대를 받았다. 한꺼번에 많은 이미지를 불러오기 때문에 FCP 시간도 빨간색이 떴다.

Next.js 공식 문서에 따르면 <Image> 컴포넌트의 사용은 이미지 최적화를 해준다. 사이즈 최적화, 시각화 안정성, 빠른 페이지 로드, 에셋 유연성을 가능하게 해준다. HTML <img /> 태그보다 더 좋은 기능을 제공하는데 안쓸 이유가 없다.

### 예시 코드

```tsx
import Image from 'next/image';

export default function Page() {
  return <Image src="./me.png" alt="Picture of the author" width={500} height={400} />;
}
```
