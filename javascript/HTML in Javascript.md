# HTML in Javascript

### document.getElementById()
document.getElementById()는 html에서 특정 id 값을 가지고 올 수 있게 해준다.

```javascript
const title = document.getElementById("title")

console.dir(title)

// title이라는 변수에 html의 title이라는 id의 정보를 불러와 console.dir()로 그 id의 특징을 오브젝트로 나누어 설명한다
```


### title.innerText

title.innerText는 getElementById()로 가져온 정보의 값을 변경 할 수 있다
```javascript
const title = document.getElementById("title") // id가 title이라는 속성을 가져오기

title.innerText = "got you!" //id가 title이라는 속성의 innerText의 값을 got you로 변경

console.log(title.id) // title이라는 변수의 id의 이름 가져오기
```
