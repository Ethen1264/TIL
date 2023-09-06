# fetch Api
- fetch() : 요청지 주소, method headers 등 요청정보, 데이터 정보(body)

- then() : 첫번째 then. 받을 데이터 형태의 빈깡통으로 세팅.  ---> 나머지 랜더링을 계속 진행

- then() : 두번째 then. 실제 데이터가 담기는 곳. ---> 랜더링 완료 후 두번째 then에 데이터가 있으면 다시 랜더링이 일어남.


### fetch 함수란 

fetch 함수는 JavaScript에서 제공하는 API 중 하나로, 서버에서 데이터를 가져오기 위해 사용됩니다.<br/>
쉽게 말하면 fetch API는 백엔드 서버와 데이터를 주고받는데 사용한다. 간단하게 설명하자면 React에서는 
Node.js 등과 데이터를 주고받기 위해 fetch 함수를 사용한다.

### method

#### Create = POST
create는 서버에 정보를 올려달라는 요청이다. ( 생성 )

create는 POST 메서드를 사용해 해당 URI를 요청하면 리소스를 생성한다.

#### Read = GET
read는 서버에서 정보를 불러오는 요청이다. ( 읽기 ) 

read는 GET 메서드를 사용해 리소스를 조회합니다. 리소스를 조회하고 해당 도큐먼트에 대한 자세한 정보를 가지고 온다.

#### Update = PUT
update는 정보를 바꾸는 요청이다. ( 수정 ) 

update는 PUT 은 데이터 전체를 바꾸고 싶을 때, PATCH는 데이터의 일부만 수정하고 싶을 때 사용한다.

#### Delete = DETELE
delete는 정보를 지우는 요청이다. ( 삭제 )

delete는 DELETE 메서드를 사용해 리소스를 삭제할 수 있다.

### headers
headers 는 Request Header를 지정해주는 곳인데, 2가지 형식으로 넣을 수 있다.
Object lireral과 Headers 객체의 인스턴스를 넣을 수 있다.

``` jsx
const req = new Request('/api/posts', {
  method: "GET",
  headers: {
    'content-type': 'application/json',
  }
});
const req2 = new Request('/api/posts', {
  method: 'GET',
  headers: new Headers({
   'content-type': 'application/json',
  })
})
```

### body
body는 HTTP Request에 실을 데이터인데 여러가지 타입을 넣을 수 있다.
즉, 전달하고자 하는 응답 내용이다. 백엔드와 통신할 때는 객체로 통신하기 때문에 객체타입으로 작성해야 한다.