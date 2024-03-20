# Metadata

### Meta 데이터란?

Meta데이터는 `<head>`에 들어가는 내용으로 유저들에게 보여지진 않지만 웹페이지의 안 보이는 부분을 담당한다.

### Meta 데이터 적용하기

찻번째로 아래와 같이 루트레이아웃에 적용할 수 있다.

#### RootLayout

```jsx
export const metadata = {
  title: {
    template: 'Home | Next Movies',
  },
  description: 'The best movies on the best freamworks',
};

export default function RootLayout() {
  // ...
}
```

만약 이와 같이 적용하면 모든 페이지의 title과 설명이 루트 레이아웃과 같아진다.

만약 루트레이아웃과 다르게 하고 싶은 페이지가 생긴다면 그냥 해당 페이지의 page.tsx 에서 metatdata 객체를 추가해주면된다. 

#### About us
```jsx
export const metadata = {
  title: 'About us',
};
```

이렇게 된다면 위의 페이지에선 `title`이 About us로 바뀌게 된다.

하지만 이제 우리가 페이지가 100개가 넘는 사이트를 만든다고 가정하자 그렇다면 저렇게 하나씩 meta데이터를 적용할 수 있을까? 이런 고민을 해결하기 위해 아래와 같이 특별한 방법이 나타났다. 

#### RootLayout

```jsx
export const metadata = { 
  title: {
    template: "%s | Next Movies",
    default: "Next Movies"
  },
  description: 'The best movies on the best freamworks',
}
```
우선 루트레이아웃이 특정 페이지의 제목을 넣기위해 `%s`를 만들어준다. 그후 내가 원하는 페이지의 파일에 들어가 아래와 같이 사용 하면된다. 

```jsx
export const metadata = {
  title: 'Home',
}
```

이렇게 적용하면 `home`이라는 페이지에 들어갔을 때 이름이 `%s | Next Movies`가 아닌 `Home | Next Movies`으로 변경된다.

### 주의점
meta data는 `use client`로 동작할 시 상요할 수 없다.