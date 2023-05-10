# Functiton

**함수(function)** 란 하나의 특별한 목적의 작업을 수행하도록 설계된 독립적인 블록을 의미한다.
이러한 함수는 필요할 때마다 호출하여 해당 작업을 반복해서 수행할 수 있다.<br>
``` javascript
function [함수명](){
  //code
}
```
**함수** 는 이러한 형태를 가지고 있으며
``` javascript
function printHello(){
  console.log("hello");
}
```
``` javascript
function addNum(x, y) { 

    console.log(x + y);

}

addNum(2, 3); 
```
이런식으로 사용할 수 있다. <br>

또 **Objects** 랑 함수랑 함께 쓸수도 있다.
``` javascript
const player = {
  name:"nico",
  sayHello: function(otherPersonName){
    console.log("hello " + otherPersonName + " nice to meet you");

  },

};
console.log(player.name);
player.sayHello("lynn");
```