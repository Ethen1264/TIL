# Returns

여태 공부한 **function**은 함수가 호출하는 시점에 함수가 선언된 곳으로 데이터를 저장하는 방법을 이용하여 **function**을 이용했었다.<br> 이번엔 함수에서 함수를 호출한 곳으로 데이터를 전송하는 방법을 이용한 **function**을 활용 했다.

```javascript
const age = 96;
function calculateKrAge(ageOfForeigner){
  return ageOfForeigner + 2;
}

const krAge = calculateKrAge(age);

console.log(krAge); 

```

```javascript
const calculator = {
  plus: function(a,b){
    return a + b;

  },
};

const plusResult = calculator.plus(2, 3);

console.log(plusResult)
```

두 예시를 비교해 보면 둘 다 함수 안에 **return**이라는 값이 들어가 있다. **return**은 함수에서 계산한 값을 **return**을 이용해 함수를 호출한 부분으로 들어가 새로 만든 변수에 저장하여 활용할 수 있다.

```javascript
const age = 96;
function calculateKrAge(ageOfForeigner){
  return ageOfForeigner + 2;
}

const krAge = calculateKrAge(age);

console.log(krAge); 
```
이 예시 처럼 

calculateKrAge(age)라는 함수에 age인 96이 들어가고 ageOfForeigner는 96으로 대체가 된다 그후 ageOfForeigner + 2의 결과를 return을 이용해 함수를 호출한 calculateKrAge(age)에 저장이 된다. 이 calculateKrAge(age)는 새로 만든 krAge라는 변수에 들어가게 된다.