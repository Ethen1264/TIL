# 모듈 내보내고 가져오기


### 선언부 앞에 export 붙이기

변수나 함수, 클래스를 선언할 때 맨 앞에 export를 붙이면 내보내기가 가능하다
```JSX
// 배열 내보내기
export let months = ['Jan', 'Feb', 'Mar','Apr', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];

// 상수 내보내기
export const MODULES_BECAME_STANDARD_YEAR = 2015;

// 클래스 내보내기
export class User {
  constructor(name) {
    this.name = name;
  }
}
```

### 선언부와 떨어진 곳에 export 붙이기

선언부와 export가 떨어져 있어도 내보내기가 가능하다.

```JSX
unction sayHi(user) {
  alert(`Hello, ${user}!`);
}

function sayBye(user) {
  alert(`Bye, ${user}!`);
}

export {sayHi, sayBye}; // 두 함수를 내보냄
```

### Export ‘as’

as를 사용하면 이름을 바꿔서 내보낼 수 있다.

``` JSX
export {sayHi as hi, sayBye as bye};
```

### import ‘as’
as를 사용하면 이름을 바꿔서 모듈을 가져올 수 있다.
sayHi를 hi로, sayBye를 bye로 이름을 바꿔서 
```JSX
import {sayHi as hi, sayBye as bye} from './say.js';

hi('John'); // Hello, John!
bye('John'); // Bye, John!
```

### export default

export default를 사용하면 '해당 모듈엔 개체가 하나만 있다’는 사실을 명확히 나타낼 수 있다.

``` JSX
export default class User { // export 옆에 'default'를 추가해보았습니다.
  constructor(name) {
    this.name = name;
  }
}
```

이렇게 default를 붙여서 모듈을 내보내면 중괄호 {} 없이 모듈을 가져올 수 있다.

``` JSX
import User from './user.js'; // {User}가 아닌 User로 클래스를 가져왔습니다.

new User('John');
```
