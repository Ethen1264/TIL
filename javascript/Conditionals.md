# Conditionals

**prompt**은 웹사이트에 글을 적을 수 있는 공간을 만들어주는 함수로 
```javascript
prompt("How old are you?");
```
이런식으로 사용할 수 있다. 하지만 최근엔 잘 사용하지 않는 함수이다. <br>

**typeof**는 수의 종류를 할 수 있게 해주는 역학을 하는데 
```javascript
console.log(typeof age);
```
이런식으로 사용할 수 있다.


**parseInt** 함수는 string형태의 문자를 number 형태로 바꿔주는 역할을 한다. 
```javascript
const age = prompt("how old are you")

console.log(age, parseInt(age))

실행결과:
15이외의 다른 수를 적으면 string이 출력 되고 15를 적으면 number가 출력됨 이외에도 숫자가 아닌 문자를 적으면 NaN이 출력됨
```

