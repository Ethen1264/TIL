# husky setting

### husky란?

Husky란 eslint나 prettier와 같은 설정을 자동화를 통해 특정 상황에서 무조건 적용이 되도록 도와주는 도구이다.
만약 Husky가 없다면 eslint, prettier와 같은 규칙을 설정해도 작업자가 사용을 하지 않으면 소용이 없다.

- 1. commit 전에 prettier formatting이 잘 적용 되어있는지 검사
- 2. push 전에 eslint 규칙이 적용 되었는지 검사

### Husky의 역할

- git hook 역할
  - git에서 특정 이벤트 발생하기 전, 후로 특정 hook 동작을 실행할 수 있게 한다. (ex. commit, push)
- git hook 설정은 까다로우며 모든 팀원들이 사전에 repo를 클론받고 메뉴얼하게 사전 과정을 수행해야지만 hook이 실행됨을 보장할 수 있다.
  - 실수로라도 사전 과정을 시행하지 않는다면 hook이 실행되지 않다.

### git hook 적용하기

```tsx
yarn add husky --save-dev
```

이후에 clone 받아서 사용하는 사람들은 yarn install후에 자동으로 husky install 이 될 수 있도록 하는 설정을 해야한다.

#### // package.json

```tsx
{
  "scripts": {
    "postinstall": "husky install"
  }
}
```

### scripts 설정

```tsx
// package.json

{
  "scripts": {
    "postinstall": "husky install",
    "lint": "eslint src --ext ts,tsx --report-unused-disable-directives --cache",
    "lint-staged": "lint-staged"
  },
  "lint-staged": {
    "**/*.{tsx,ts,jsx,js}": ["prettier --write"]
  }
}

```

### add pre-commit, pre-push hook

```
npx husky add .husky/pre-commit "yarn lint-staged"
```

```
npx husky add .husky/pre-push "yarn lint"
```

해당 명령어를 입력하면 루트 위치에 .husky 폴더가 생성된다.

### lint-staged 설치 (prettier 검사)

포맷팅을 수행 한 뒤 git add 명령어를 자동으로 수행되게 할 수 있다.
포맷팅을 전체 파일 대상이 아닌 현재 git stage에 올라온 변경사항 대상으로만 수행할 수 있다.

```tsx
yarn add -D lint-staged

```

### gitignore에 .eslintcache 파일 추가

```tsx
.eslintcache
```
