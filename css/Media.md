# Media

### 사용하는 이유

미디어 쿼리는 CSS에서 어떤 스타일을 선택적으로 적용하고 싶을 때 사용합니다. 즉 특정 사이즈가 되었을 때 화면의 정렬 방법, 방향, 등을 수정하여 반응형으로 만들 수 있다.

### 기본 형태

```css
@media (조건) {
  스타일
}
```

### 좁은 화면 스타일

800px 이하의 좁은 화면에서 특정 HTML 요소의 배경색을 토마토 색으로 바꾸고 싶다면,

```html
<div class="small-tomato">좁은 화면에서는 배경색이 토마토 색이 됩니다.</div>
```

```css
@media (max-width: 800px) {
  .small-tomato {
    background-color: tomato;
  }
}
```

사이즈가 800px 보다 작을시 배경의 색이 토마토 색으로 변하게 된다.

### 넓은 화면 스타일링

800px 이상의 넓은 화면에서 특정 HTML 요소의 글자색을 토마토 색으로 바꾸고 싶다면,

```html
<div class="large-tomato">넓은 화면에서는 글자색이 토마토 색이 됩니다.</div>
```

```css
@media (min-width: 800px) {
  .large-tomato {
    color: tomato;
  }
}
```

사이즈가 800 보다 커지면 배경의 색이 토마토 색으로 변하게 된다.
