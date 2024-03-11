# NextJsRule

- next는 프론트엔드 서버이다

- next에서 구상하는 page는 pages 폴더에 만들어야 한다, page에 만들 파일들을 파일명에 대하여 endpoint 생기고 자동으로 next에서 code splitting을 해준다

- 폴더를 만들고 그 안에 파일을 만들면 주소 구성을 자동으로 해준다. pages안에 "./first/second.js"로 만들었을 경우 endpoint는 domain/first/second가 된다

- 페이지 이동 시 a 태그가 아닌 Link 태그로 a 태그를 감싸고 Link 태그에 href 속성을 적용하여 endpoint를 적어줘야 함

- 프론트서버와 백엔드서버의 주소가 다르기 때문에 cors 설정을 해줘야 데이터를 주고 받을 수 있다

- _app.js는 모든 페이지의 공통적인 부분을 담당하며 page들의 return 부분이 _app.js props인 Component로 들어가는 것이다. 페이지에 공통적으로 추가하고 싶은 부분은 _app.js에 선언하면 된다. ( CSS 라이브러리, Redux...)

- <head> 태그의 <title>를 next에서 수정하고 싶은 경우 next에서 head 컴포넌트를 제공한다 

- next-redux-wrapper는 next에서 reudx의 사용을 편리하게 해주는 라이브러리이다

- createWrapper에서 debug를 true로 해놓으면 redux 개발 시 문제를 시각화해주기에 개발이 편리하다

- next에서 redux 사용 시 <Provider>로 루트 컴포넌트를 감싸줄 필요가 없다