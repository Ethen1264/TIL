# classList & className

classList & className이 두가지를 이용해 클래스를 조종해 css의 디자인을 변경 할 수 있다. className은 원래 클래스가 있다면 그 클래스를 삭제하고 추가 하지만 classList는 클래스를 하나 더 추가하는 방식이다.

```javascript
const h1 = document.querySelector(".hello h1")


function handleTItleClick() {
  const clickedClass = "active"
  if(h1.classList.contains(clickedClass))
  {
    h1.classList.remove(clickedClass)
  } else {
    h1.classList.add(clickedClass)
  }
}
h1.addEventListener("click", handleTItleClick)
```
classList를 사용하면 이런식으로 클릭 했을 때 클래스를 추가할 수 있다. 또한 toggle() 이라는 함수를 쓰면 더욱 간결하게 만들 수 있는데

``` javascript
const h1 = document.querySelector(".hello h1")


function handleTItleClick() {
  h1.classList.toggle("active")
}
h1.addEventListener("click", handleTItleClick)

```

toggle()는 해당 클래스가 없다면 추가하고 있다면 삭제할 수 있는 기능을 가지고 있다.