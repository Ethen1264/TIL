# scss

Syntactically Awesome StyleSheet의 약어이며, CSS를 효율적으로 작성할 수 있도록 도와주는 전처리기
SASS, SCSS에서 기존의 CSS의 기능 부재 단점을 보완한 다양한 기능 추가 되었다.

scss 를 검색하면 그와 동시에 sass 에 대한 글도 많이 보인다. 이 둘은 어떤 차이점이 있을까?

### sass vs scss 의 차이점?

scss는 Sass(Syntactically Awesome Style Sheets)의 3버전에서 새롭게 등장 하였다. CSS 구문과 완전히 호환되도록 새로운 구문을 도입해 만든 Sass의 모든 기능을 지원하는 CSS의 상위집합(Superset) 이다. SCSS는 CSS와 거의 같은 문법으로 Sass 기능을 지원한다.

### 구문 스타일

Scss : {} 중괄호 와 , ; 세미콜론을 사용한다.
Sass : 중괄호가 아닌 들여 쓰기를 사용

- ex) scss

```css
.background {
  width: 100px;
  float: left;
  li {
    color: red;
    &:last-child {
      background-color: yellow;
    }
  }
}
```

- ex) sass

```css
.background
  width: 100px;
  float: left;
  li
    color: red;
    &:last-child
     background-color:yellow;
```

### mixin 문법

styled-component 를 사용할때 , 중복된 스타일을 방지 하기 위해
중복되는 스타일 코드들만 컴포넌트로 뺄수 있었다는게 가장 큰 장점으로 느꼈다.
하지만 scss 도 @mixin이라는 문법을 사용하여 중복되는 스타일을 따로 작성하고,
@include 로 필요한 부분에 넣을수 있었다.

Scss : @mixin 으로 선언하고 @include 로 적용시킨다.
Sass : = 로 선언하고 + 로 적용시킨다.

```css
@mixin ButtonComponent {
  text-align: center;
  width: 300px;
  height: 200px;
  background-color: black;
}

.button {
  @include ButtonComponent {
    color: white;
  }
}
```
