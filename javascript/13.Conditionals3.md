# Conditionals

* 조건문은 if, else if, else 이렇게 나누어 짐<br>
* 조건문안에 &&, ||을 사용할 수 있는데 && 모든 값이 true여야 성립하고 ||은 여러 값중 하나의 값만 true면 true로 성립한다.

``` javascript
const age = parseInt(prompt("How old are you?"))

console.log(isNaN(age))
  
if(isNaN(age) || age < 0) {                  
  console.log("please write a number")    //age의 값이 숫자가 아니거나 양수가 아니면 출력
} else if(age < 18) {
  console.log("you are too young")        //age의 값이 18미만이면 출력
} else if (age >=18 && age <=50 ){
  console.log("you can drink")            //age의 값이 18살 이상 50살 이하라면 출력
} else if(age > 50 && age <=80) {
  console.log("you should exercise")      //age의 값이 50살 이상 80살 이하면 출력
} else if (age > 80){                     
  console.log("you can do whatever you want") //age의 값이 80살 초과면 출력
}else {
  console.log("you can't drink")          //위의 값이 모두 성립하지 않으면 출력
} 
```