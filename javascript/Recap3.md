# Recap 2

## Object

**object**는 **array**와 달리 연관되어 있는 property들을 그룹을 묶어서 저장해야 할 떄 사용한다.<br>

``` javascript
const player = {
  name: "Nico",
  age: 98,
};

console.log(player);
player.name = "nicolas"; // object의 값을 바꿔준다
console.log(player);
player.boy = "true" //object의 값을 추가해준다
console.log(player);
```

## function

**function**은 어떤 코드를 캡슐화해서 그걸 반복해서 사용할 수 있도록 만든 것 을 함수라고 한다

```javascript
function plus(a, b){
  console.log(a+b);
}
plus(5, 10) // plus 함수로 5와 10이 들어가 a는 5가 b는 10이 저장이 되어 5 + 10 = 15가 출력이 된다
```

<hr>
오늘 공부한 **object**와 **function**을 사용하여 이러한 예제를 만들 수 있다

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

