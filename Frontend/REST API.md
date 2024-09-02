# REST API

### REST API란?

- REST(Representation State Transfer)의 약자로 요청된 주소만 보고도 어떤 내용에 관한 요청인지 예상할 수 있게 하는 형식을 말한다.
- REST는 자원(Resource)을 URI로 표현하고, HTTP 메서드(GET, POST, DELETE, PUT, PATCH)를 사용해서 해당 자원의 CRUD를 적용하는 것을 의마한다.
- 즉 네트워크상에서 Client와 Server 사이의 통신하는 방식 중 하나이다.
- 이런 REST의 기본 원칙을 성실히 지킨 서비스 디자인을 RESTful라고 표현하며, REST API는 REST 아키텍처 스타일을 따르는 API를 의미한다.

### REST API 의 구체적인 개념

- REST API는 자원, 행위, 표현의 3가지 요소로 구성되어 있다.
- URI를 통해 자원을 명시하고, HTTP 메서드 (GET, POST, DELETE, PUT, PATCH)를 통해 해당 자원에 대한 CRUD를 적용하는 것을 의미한다.
- 웹의 모든 자원에는 고유한 ID인 HTTP URI가 있다.

> 자원(Resource): URI
>
> 행위(Verb): HTTP 요청 메서드 (GET, PUT, DELETE, POST, PATCH)
>
> 표현(Representations): 행위에 대한 구체적 내용

### RESTful API가 중요한 이유

- 플랫폼 간 호환성: 최근의 서비스 / 애플리케이션의 개발 흐름은 멀티 플랫폼, 멀티 디바이스 시대로 넘어왔다. 단순히 하나의 브라우저만 지원하면 되었던 이전과는 달리 이제는 다양한 통신에 대응할 수 있어야 한다. RESTful API는 HTTP를 기반으로 하기 때문에 플랫폼에 독립적입니다. 이는 서로 다른 프로그래밍 언어나 프레임워크를 사용하는 애플리케이션 간의 통신을 용이하게 한다.

- 확장성과 유지보수성: RESTful API는 자원 중심적인 아키텍처를 가지고 있어, 새로운 리소스를 쉽게 추가하거나 기존 리소스를 수정할 수 있다. 또한 상태를 유지하지 않는(stateless) 아키텍처를 갖추고 있기 때문에 서버의 부하를 줄이고 확장성을 향상시킨다.

> 따라서 HTTP 표준 규약을 지키면서 API를 통신하는 방법이 매우 중요해졌다.

### 자원(Resource) - URI

모든 자원에는 고유한 URI가 존재하고 이 자원은 서버에 존재한다. 클라이언트는 URI를 이요앻서 필요한 자원을 지정하고 해당 자원의 정보를 서버에 요청할 수 있다.

예를들어
GET/todos:todos의 데이터를 서버에 요청해서 가져온다.
DELETE/todos/1:todos중에서 id 1번을 가진 데이터를 서버에 요청해 지운다.

> URL과 URI의 차이점
>
> URL은 Uniform Resource Locator로 인터넷 상 자원의 위치를 의미한다.
>
> URI는 자원의 위치뿐만 아니라 자원에 대한 고유 식별자로서 URL의미를 포함하는 더 넓은 범위이다.

- https://naver.com 의 경우, 자원의 위치를 의미하기에 URL 이면서 URI 이다.
- https://comic.naver.com/webtoon 의 경우 comic.naver 서버의 webtoon 라는 위치를 의미하기에 URL 이면서 URI 이다.
- https://comic.naver.com/webtoon/list?titleId=796152&tab=tue 의 경우는 조금 다르다. URL 는 https://comic.naver.com/webtoon 까지이고, 내가 원하는 사이트에 들어가기 위해서는 titleId=796152 라는 특정한 식별자가 필요하다. 즉 위 주소는 URI 이지만 URL 은 아니다.

### 행위 - HTTP 요청 메서드

HTTP 요청 메서드는 클라이언트가 서버에게 요청의 종류와 목적을 알리는 방법이다. 주로 5가지 요청 메서드 `GET, POST, DELETE, PUT, PATH`를 사용해서 CRUD를 구현한다.

### 표현 - 페이로드(payload)

클라이언트와 서버가 데이터를 주고 받는 형태로 JSON, XML, TEXT, RSS 등이 있다. JSON, XML을 통해 데이터를 주고 받는 것이 일반적이다.

### REST API의 특징

#### Uniform (유니폼 인터페이스)

Uniform Interface는 URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일을 말한다.

#### Stateless (무상태성)

REST는 작업을 위한 상태정보를 따로 저장하고 관리하지 않는다. 세션 정보나 쿠키정보를 별도로 저장하고 관리하지 않기 때문에 API 서버는 들어오는 요청만을 단순히 처리하면 된다. 그렇기에 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로 구현이 단순해진다.

#### Self=descriptiveness (자체 표현 구조)

REST의 또 다른 큰 특징 중 하나는 REST API 메시지만 보고도 이를 쉽게 이해 할 수 있는 자체 표현 구조로 되어 있다는 것이다. HTTP 헤더와 HTTP 메서드, 그리고 URI를 통해서 어떤 요청인지 명확히 구분할 수 있다.

#### Client - Server 구조

REST 서버는 API 제공, 클라이언트는 사용자 인증이나 컨텍스트(세션, 로그인 정보)들을 직접 관리하는 구조로 각각의 역할이 확실히 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로간 의존성이 줄어든다.

#### 계층형 구조

REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드밸런싱, 암포화 계층을 추가해 구조사으이 유연성을 둘 수 있고 Proxy, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있게 한다.

### 결론

REST는 클라이언트와 서버간의 통신 방식을 규정한 아키텍처로 모든 자원은 고유한 URI로 명시하고, HTTP 메서드인 GET, POST, DELETE, PUT, PATCH를 통해 해당 자원에 대한 CRUD를 적용한다.

이러한 방식은 클라이언트와 서버 간의 통신을 단순화 시켜둔다는 장점이 있으며, 또한 상태를 저장하지 않고 요청에 대한 응답만 내려주기 때문에 서버의 부하를 줄일 수 있다는 장점도 있다.
