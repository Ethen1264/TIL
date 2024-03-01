# ViteJs

### vite란?

Vite는 프랑스어로 '빠르다'라는 뜻을 가진 단어이다. 이러한 vite라는 이름처럼 빌드와 개발 서버 구동 시간이 매우 빠릅니다. 기존에 자주 사용하던 webpack, rollup 등의 빌드 도구는 자바스크립트 언어로 만들어졌지만, Vite가 내부적으로 사용하는 ESBuild는 Go라는 네이티브 언어로 만들어진 도구를 이용해 빌드하기 때문에 빌드 속도가 아주 빠르다.

### vite의 장점

기존의 번들러 기반으로 개발을 진행할 때, 소스 코드를 업데이트 하게 되면 번들링 과정을 다시 거쳐야 했다. 이처럼 서버가 큰 환경일수록 갱신시간이 증가하게 된다. 이 부분을 해결하기 위해 ESM + HMR을 이용하게 되었다. 이것을 사용하면 vite는 수정된 부분만 수정된 모듈을 교체한다. 또한 vite는 HTTP 헤더를 활용하여 전체 페이지의 로드 속도를 높인다.

### vite 다운로드

#### npm

`npm create vite@latest`

#### yarn

`yarn create vite`

#### pnpm

`pnpm create vite`


### 빌드 명령어 

```
1. npm run build 
2. yarn build
```
 

### 개발 서버 시작 명령어

```
1. npm run dev
2. yarn dev
```