# title.addEventListener()

title.addEventListener() 란 사용자의 행동을 반응해서 어떻게 변화할지 정하는 함수이다.

```javascript
const title = document.querySelector(".hello h1") //title이라는 변수에 hello라는 클래스와 h1이라는 태그를 가지고 있는 속성을 대입한다.

function handleTItleClick() {
  title.style.color= "red"    // title이라는 변수의 색을 red로 변경하는 함수를 만든다
}


title.addEventListener("click", handleTItleClick) // 사용자가 click을 하면 handleTItleClick라는 함수가 실행되게 한다.
```

위에 배운 것을 활용하면 이런 식으로 활용할 수도 있다
``` javascript
const h1 = document.querySelector(".hello h1")

console.dir(h1)

function handleTItleClick() {
  h1.style.color= "red"
}
function handleMouseEnter() {
  h1.innerText = "Mouse is here"
}
function handleMouseLeave() {
  h1.innerText = "Mouse is gond"
}

function handleWindowResize() {
  document.body.style.backgroundColor = "tomato"
}
function handleWindowCopy () {
  alert("copier!")
}
h1.addEventListener("click", handleTItleClick)
h1.addEventListener("mouseenter", handleMouseEnter)
h1.addEventListener("mouseleave", handleMouseLeave)

window.addEventListener("resize", handleWindowResize)
window.addEventListener("copy", handleWindowCopy)
```