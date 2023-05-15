# Recap

## variables
js에 Variables에는 **const** **let** **var**이 있다. <br>
**const**는 변수의 값을 바꿀 수 없지만 <br> 
**let**는 변수의 값을 바꿀 수 있다.<br>
**var** 보안 문제로 사용하지 않는다
<br>
<br>

이때 변수에 저장할 수 있는 또 다른 예시에는 **null** 과 **undefined**가 있는데 <br> 
**null**은 비어있다 라는 뜻이며 **undefined**는 정의되어 있지 않다. 라는 뜻이다 

<hr>

## array
 배열로 많은 변수를 한번에 선언하기 위해 사용된다.
``` javascript
const toBuy = ["potato", "tomato", "pizza"];
console.log(toBuy[2]);

결과: pizza
```
``` javascript
const toBuy = ["potato", "tomato", "pizza"];
console.log(toBuy);
toBuy[2] = "water";
console.log(toBuy);


결과: "potato", "tomato", "pizza"
      "potato", "tomato", "water"
```

``` javascript
const toBuy = ["potato", "tomato", "pizza"];
console.log(toBuy);
toBuy[2] = "water";
console.log(toBuy);
toBuy.push("meat");
console.log(toBuy);

결과: "potato", "tomato", "pizza"
      "potato", "tomato", "water", "meat"
```
