# Array

### Array는 배열로 많은 변수를 한번에 선언하기 위해 사용된다. <br>
배열은 **[ ]** 리터럴 대괄호를 사용하는데
<hr>

### .length 

``` javascript
const numbers = [1,2,3,4]
const fruits = ["apple", "banana", "cherry"]

//.length는 배열의 갯수를 센다
console.log(numbers.length) //4출력
console.log(fruits.length)  //3출력
console.log([1,2].length)   //2출력

console.log([].length)      //0출력
```
``` javascript
let arr = []; 

arr[0] = 'zero';
arr[1] = 'one';
arr[2] = 'tow';

for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}    
```
``` javascript
let arr = ['zero', 'one', 'tow']; 

for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}
```
이런식으로 사용할 수 있다. <br>
**이떄 Array의 자릿수는 0부터 시작한다.**

<hr>

### .push

또 배열 안에 값을 추가할 수 있는데 **push**를 사용하여 추가할 수 있다.

``` javascript
let arr = ['zero', 'one', 'tow']; 

arr.push("three");
console.log(arr);
```

### .concat 
```javascript
const number = [1, 2, 3, 4]
const fruits = ['Apple', 'Banana', 'Cherry']

console.log(number.concat(fruits))  // 두개의 배열을 결합 한다 [1, 2, 3, 4, "Apple", Banana", Cherry]
console.log(number)     // [1, 2, 3, 4]
console.log(fruits)     // ['Apple', 'Banana', 'Cherry']

```

### .forEach
```javascript

// .forEachㄹㄴ 콜백 함수를 받는다

const number = [1, 2, 3, 4]
const fruits = ['Apple', 'Banana', 'Cherry']

fruits.forEach(function (element, index, array) {   // fruits.forEach(function (요소, index, array는 거의 사용 안함)순서로 반복되는 아이템 반복되는 횟수 순서로 나타난다 
    console.log(element, index, array)
})

```javascript

const myArr = [1, 2, 3, 4, 5];

myArr.forEach((currentElement, index, array) => {
    console.log(`요소: ${currentElement}`);
    console.log(`index: ${index}`);
    console.log(array);
});

```
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbtpHUl%2FbtqFVi8aW0t%2FNtNMk8SnBbhIk7dWJisAS0%2Fimg.png)

### map

```javascript
const number = [1, 2, 3, 4]
const fruits = ['Apple', 'Banana', 'Cherry']

const a = fruits.forEach(function (fruit, index) {
    console.log("${fruit}-${index}")
})
console.log(a)

const b = fruits.map(function (fruit,index) {
    return "${fruit}-${index}"
})
console.log(b)

//map은 콜백의 내부에서 반환하는 하나의 데이터를 가지고 새로운 배열을 만들어 반환한다
```