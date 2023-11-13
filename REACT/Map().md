# map()

```map()```함수는

``` JSX
[1,2,3].map(function(){})
```

이러한 형태를 가지고 있으며 소괄호 안에 들어있는 함수들은 다 콜백 함수이다.

### map() 사용법

1. array 자료 갯수만큼 함수안의 코드 실행해줌

``` JSX
[1,2,3].map(function(){
	console.log(1)
})
```

![Alt text](https://velog.velcdn.com/images/4775614/post/53870299-9915-48ad-976d-1804ebaa3bc6/image.png)

2. 함수의 파라미터는 array안에 있던 자료 파라미터를 하나를 a라고 해주고 찍어보면 array안에 있던 자료 하나하나의 데이터가 된다. 코드가 반복실행 되면 1이되고 2가되고 3이된다.

``` JSX
[1,2,3].map(function(a){
	console.log(a)
})

```

![Alt text](https://velog.velcdn.com/images/4775614/post/729d83ce-bd64-4682-82ac-12b203ba7168/image.png)

3. return에 내용을 적으면 array로 받아 array 갯수만큼 받아주니까 3번이 찍힘

``` JSX
[1,2,3].map(function(a){
	return '1233211'
})
```

![Alt text](https://velog.velcdn.com/images/4775614/post/692f71e6-5c83-4490-a466-d84597d4122f/image.png)


## KEY

key는 react가 어떤 항목을 변경,추가 또는 삭제할지 식별하는 것을 돕는다.
``` JSX
<li key = {}> 내용 </li>
```

### 컴포넌트 사용시 map함수에서 key 사용법

```key```는 ```element```에 안정적인 고유성을 부여하기 위해 배열 내부의 엘리먼트에 지정해야한다.

``` JSX
const contentComments = {[
        {
          'id'  : 0,
          'name': 'chanho',
          'text': '안녕하세요 테스트 중입니다!😝'
        }, {
          'id'  : 1,
          'name': 'hoho',
          'text': '위코드으~~😀😀😀😀'
        }];
}
contentComments.map((list) =>
  <li key={list.id}>
    {list.name}
    {list.text}
  </li>
);
```

```index```에 ```key```값을 부여할 수 있다 하지만 이로인해 성능이 저하되거나 state와 관련된 문제가 발생할 수 있다 