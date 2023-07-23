# string

### String.prototype.indexOf()
String.prototype.indexOf()는 indexOf() 메서드는 호출한 String 객체에서 주어진 값과 일치하는 첫 번째 인덱스를 반환하고 일치하는 값이 없으면 -1을 반환한다.

```javascript
const result = 'Hello world'.indexOf('world')
console.log.(result)
//Hello world라는 글에 world라는 말이 있으니까 world의 시작 부분인 6출력
```

```javascript
const result = 'Hello world'.indexOf('hi')
console.log(result)
// Hello world라는 글에 hi라는 말이 없으니까 -1출력
```

### .length
.length는 문자열의 개수를 읽는 역할을 한다.
```javascript
const str = "0123"

console.log(str.length)
// 0123의 개수를 하나씩 세서 4가 출력
```

### .slice
slice() 메소드는 문자열의 일부를 추출하면서 새로운 문자열을 반환합니다.

```javascript
const str = "Hello world"
console.log(str.slice(0,3))
// 시작부분인 0부터 끝부분인 3의 직전 2까지 출력한다 즉 0인 H부터 3의 직전 2인 l까지 출력 = Hel
```

### .replace
.replace는 특정 부분의 값을 다르게 변환 한다.

```javascript
const str = "Hello world"

console.log(str.replace("world", "hi"))
// hello world에서 world를 찾아 world의 값을 hi로 변환한다 = Hello hi
```

### .trim
.trim은 문자 데이터 앞 뒤의 공백을 제거한다.

```javascript
const str = "   hello world   "

console.log(str.trim())
//"   hello world    "라고 출력되는 것이 아닌 "hello world"라고 출력 된다
```