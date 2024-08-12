# style

### style

```tsx
export const container = style({
  display: 'flex',
  flexDirection: 'column',
  backgroundColor: global.background.color,
  width: '100dvw',
  height: '100dvh',
  padding: 36,
  '@media': {
    '(min-width: 1000px)': {
      flexDirection: 'row',
      padding: 0,
    },
  },
});
```

위와 같이 style로 감싼 후 적용할 태크에 아래와 같이 지정해주면 된다.

```tsx
import { ReactNode } from 'react';
import * as styles from '@/app/(beforeLogin)/_component/main.css';

type Props = { children: ReactNode; modal: ReactNode };
export default function Layout({ children, modal }: Props) {
  return (
    <div className={styles.container}>
      {children}
      {modal}
    </div>
  );
}
```

### globalStyle

globalStyle은 이미 만들어둔 스타일 요소의 자식의 스타일을 지정할 때 사용한다.

```tsx
export const left = style({
  display: 'flex',
  alignItems: 'center',
  '@media': {
    '(min-width: 1000px)': {
      flex: 1,
      justifyContent: 'center',
    },
  },
});

globalStyle(`${left} img`, {
  width: 55,
  height: 65,
  '@media': {
    '(min-width: 1000px)': {
      width: 450,
      height: 550,
    },
  },
});
```

### selectors

selectors는 자기자신을 기준으로 한다. (자기 자신만 지정이 된다.)

```tsx
export const left = style({
  display: 'flex',
  alignItems: 'center',
  '@media': {
    '(min-width: 1000px)': {
      flex: 1,
      justifyContent: 'center',
    },
  },
  selectors: {
    'img &': {
      width: 55,
      height: 65,
      '@media': {
        '(min-width: 1000px)': {
          width: 450,
          height: 550,
        },
      },
    },
  },
});
```

위와 같이 지정하면 img태그의 자식인 left에 적용된다.
하지만 반대로 left의 자식 img 태그론 지정이 불가하다.

### 상태 선택자

```tsx
export const test = style({
  ':hover': {
    color: 'red',
  },
  ':disabled': { background: 'blue' },
});
```

위와 같이 사용할 수 있는데 `selectors`를 사용하면 상태 선택자를 두 경우를 합칠 수 있다.

```tsx
selectors: {
  '&:disabled:hover':{
    color: 'red'
  }
  },
```

위의 경우 test이면서 disabled이고 hover가 됐을때 적용이 된다.
