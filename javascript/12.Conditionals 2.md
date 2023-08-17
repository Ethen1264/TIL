# Conditionals


## isNaN()

isNaN()은 ()안에 들어있는 값이 문자인지 아닌지 판단하는 함수로 만약 문자라면 True가 숫자라면 False가 출력 된다.
* Not A Number라는 뜻 (숫자가 아니다)
``` javascript
const age = parseInt(prompt("How old are you"))

console.log(isNaN(age))

// age= 15 false 출력 age='abc' true 출력
```

isNaN ()을 사용해여 조건문에 활용하면
``` javascript

const age = parseInt(prompt("How old are you?"))    //prompt() 함수로 사용자에게 값을 물어보고 그 값이 123이라면 age를 숫자로 변환하고 값이 'abc'리먄 NAN으로 반환후 age에 대입
console.log(isNaN(age)) //age에 대입한 값을 출력 하는데 isNaN이 숫자가 아니면 true를 출력 숫자라면 false를 출력한다

if(isNaN(age)) { 
  console.log("please write a number")      // age에 대입한 값을 검사하는데 isNaN이 숫자가 아니면 please write a number 출력 숫자라면 thx를 출력한다
} else {
  console.log("thx")
}

```
