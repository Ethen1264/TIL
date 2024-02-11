# Object 

### 객체 타입

중괄호({})를 이용해 객체 타입(object type)을 표현할 수 있다. 

```ts
const user: { name: string; height: number; } = { name: '이다한', height: 165 };
```

이 때 객체 타입 정의는 오브젝트 리터럴과 다음과 같은 차이점이 있다.
- 구분자로 콤마(,) 뿐만 아니라 세미콜론(;)을 사용할 수 있다.

### 선택 속성

속성명 뒤에 물음표(?)를 붙여 해당 속성이 존재하지 않을 수도 있음을 표현할 수 있다.

```ts
const user: { name: string; height?: number; } = { 
  name: '이다한' 
};
```

위와 같이 **height**에 ```?```가 붙어있는 것을 볼 수 있다. 이는 **height**가 존재할 수도 있고 존재하지 않을 수도 있다는 것을 나타낸다.

### 읽기 전용 (readonly)

속성명 앞에 readonly 키워드를 붙여 해당 속성의 재할당을 막을 수 있다. 

```ts
const user: { 
  readonly name: string; 
  height: numer; 
} = { name: '안희종', height: 176 };
user.name = '종희안'; // error발생
```

error가 발생하는 이유는 ```user.name```가 readonly로 설정되어 있기 때문에 값을 수정할 수 없다.