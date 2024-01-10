# foreach  & map 

### foreach의 특징

- forEach()가 배열 요소마다 한 번씩 주어진 함수(콜백)를 실행한다.

```jsx
const arr = [1, 2, 3, 4, 5];
const arr2 = [];

arr.forEach(num => {
  arr2.push(num * 2);
});

console.log(arr2); 
// [2, 4, 6, 8, 10]
```

- foreach는 리턴 값이 존재하지 않는다.

```jsx
let arr = [1,2,3,4,5];
let num = arr.forEach(function(n){
	return n;
});
console.log(num);   //undefined
```


### map의 특징

- map()은 함수(콜백)를 호출한 결과를 모아 새로운 배열을 반환한다.

```jsx
const arr = [1, 2, 3, 4, 5];
const num = arr.map(num => num * 2);

console.log(num); 
// [2, 4, 6, 8, 10]
```

- map은 리턴값이 존재한다.

```jsx
let arr=[1,2,3,4,5];
let num = arr.map(function(n){
	return n +1;
});
console.log(num);  // [2,3,4,5,6]
```

 forEach() 기존의 Ararry를 변경하지만 map()은 새로운 Ararry를 반환한다.

성능면에서는 map이 forEach보다 빠르고 유리하다. 
