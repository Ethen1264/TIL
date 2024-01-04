# Variables

Variables는 코드를 조금 더 간결하고 수정하기 쉽게 하기 위해 사용한다. <br>
js에서의 변수를 사용하는 방법으론 3가지가 있는데 **var, let, const**가 있다.<br>
## var
``` javascript 
var num = 3;
console.log(num);
```
**var**는 이런식으로 사용하는데 언제 어디서나 값을 바꿀 수 있다는 장점도 있지만<br> 언어의 보호를 받지 못해 취약할 수 있기 때문에 권장하지 않는다.

###  var의 문제점
```js
  var string1 = "hi";
    var num = 1;

    if (num === 1) {
        var string1 = "hello"; 
    }
    
    console.log(string1 )
```
**string1 === 1**가 **true** 이기 때문에 **string1 = hello**가 됩니다.만약 의도해서 이러한 if문이 동작되게 설정한 것이라면 문제가 없지만 그렇지 않다면 뜻 밖의 코드인 **hello**가 출력 될 것 입니다.

___
## const
``` javascript 
const constant = 10;
console.log(constant);
```
**const**는 가장 많이 사용하는 변수중 하나로 변수의 값을 자유롭게 바꾸진 못한다.
___
## let
``` javascript 
let str = "a";
console.log(str);
```
**let**은 const와 같이 가장 많이 사용하는 변수인데 const와 다르게 변수의 값을 자유롭게 바꿀 수 있다.
