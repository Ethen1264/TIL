# number

### toFixed() & parseInt & parseFloat
```javascript
const pi = 3.141592
console.log(pi)   //pi인 3.141592 출력

const str = pi.toFixed(2) //toFixed()를 사용해 소숫점 2번째 자리 까지 지정
console.log(str)  //3.14출력
console.log(typeof str) //위에서 선언한게 문자열 이기 떄문에 string 풀력

const integer = parseInt(str) //문자열을 parsetInt를 사용해 숫자형으로 바꾸고 Int이기 때문에 3 지정
const float = parseFloat(str) //문자열을 parsetInt를 사용해 숫자형으로 바꾸고 float이기 때문에 3.14 지정
console.log(integer)  //3 츨략
console.log(float)    //3.14 출력
console.log(typeof integer, typeof float) //string에서 parseInt와 parseFloat으로 숫자형으로 바꿨기에 number number 출력
```

# Math

```javascript

console.log("abs:", Math.abs(-12))  // 절대값으로 발환 12

console.log("min:", Math.min(2,8))  // 두 숫자 중에서 작은 값 출력 2

console.log("max:", Math.max(2,8))  // 두 숫자 중에서 큰 값 출력 8

console.log("ceil:", Math.ceil(3.14)) // 정수 뒤에서 올림 4

console.log("floor:", Math.floor(3.14)) // 정수 뒤에서 버림 3

console.log("round:", Math.round(3.14)) // 정수 뒤에서 반올림 3

console.log("random:", Math.random()) // 랜덤 숫자 출력

```