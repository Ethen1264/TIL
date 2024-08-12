# global

### 설치 & 설정

```tsx
npm i @vanilla-extract/css
```

- nextjs일 경우

```tsx
npm install --save-dev @vanilla-extract/next-plugin
```

- next.config.js 설정

```tsx
const { createVanillaExtractPlugin } = require('@vanilla-extract/next-plugin');
const withVanillaExtract = createVanillaExtractPlugin();

/** @type {import('next').NextConfig} */
const nextConfig = {};

module.exports = withVanillaExtract(nextConfig);
```

### globalStyle 적용하기 (css 초기화)

#### 기존의 css

```css
html,
body {
  max-width: 100vw;
  overflow-x: hidden;
}
```

#### vanilla-extract

```tsx
globalStyle('html', {
  '@media': {
    '(prefers-color-scheme: dark)': {
      colorScheme: 'dark',
    },
  },
});
globalStyle('html, body', {
  maxWidth: '100dvw',
  overflowX: 'hidden',
});
```

### globalstyle Theme 적용하기

```css
@media (prefers-color-scheme: dark) {
  :root {
    --foreground-rgb: 255, 255, 255;
    --background-start-rgb: 0, 0, 0;
    --background-end-rgb: 0, 0, 0;

    --primary-glow: radial-gradient(rgba(1, 65, 255, 0.4), rgba(1, 65, 255, 0));
    --secondary-glow: linear-gradient(to bottom right, rgba(1, 65, 255, 0), rgba(1, 65, 255, 0), rgba(1, 65, 255, 0.3));

    --tile-start-rgb: 2, 13, 46;
    --tile-end-rgb: 2, 5, 19;
    --tile-border: conic-gradient(#ffffff80, #ffffff40, #ffffff30, #ffffff20, #ffffff10, #ffffff10, #ffffff80);

    --callout-rgb: 20, 20, 20;
    --callout-border-rgb: 108, 108, 108;
    --card-rgb: 100, 100, 100;
    --card-border-rgb: 200, 200, 200;
  }
}
```

기존의 방법이 아닌 vanilla-extract는 객채 형태로 뽑아서 사용해야 한다

```tsx
export const global = createGlobalThemeContract({
  background: {
    color: 'bg-color',
  },
  foreground: {
    color: 'fg-color',
  },
});

const whiteGlobalTheme = {
  background: {
    color: 'rgb(255, 255, 255)',
  },
  foreground: {
    color: 'rgb(0, 0, 0)',
  },
};

const darkGlobalTheme = {
  background: {
    color: 'rgb(0, 0, 0)',
  },
  foreground: {
    color: 'rgb(255, 255, 255)',
  },
};

createGlobalTheme(':root', global, whiteGlobalTheme);

globalStyle(':root', {
  '@media': {
    '(prefers-color-scheme: dark)': {
      vars: assignVars(global, darkGlobalTheme),
    },
  },
});
```

임포트 하기

```tsx
import './globalTheme.css';
```
