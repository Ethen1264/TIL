# document.querySelector() & document.querySelectorAll()

### document.querySelector()
document.querySelector()는 css 형식으로 값을 불러오는 방식이다 (querySelector은 태그와 클래스가 같아도 첫번째 것만 가져온다)
```javascript
const hellos = document.querySelector(".hello h1") //문서에서 hello라는 클래스의 h1태그를 가져옴

console.log(hellos) // hellos의 값을 출력함
```

### ### document.querySelectorAll()
document.querySelectorAll()은 querySelector()과 다르게 검색한 모든 태그를 가져올 수 있다.

```javascript
const hellos = document.querySelectorAll(".hello h1")

console.log(hellos)
```