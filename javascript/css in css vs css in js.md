# css in css vs css in js

### CSS-in-CSS란?

> "CSS-in-CSS"라는 용어는 전통적인 CSS 방식을 가리키는 말로, 보통은 별도의 CSS 파일에 스타일을 작성하고 이를 HTML에 연결(link)하여 사용하는 방식을 말한다.

CSS를 모듈화 한다는 의미이다. CSS 클래스를 만들면 자동으로 고유한 클래스네임을 만들어서 스코프를 지역적으로 제한한다.

CSS 모듈은 동일 프로젝트 소스 안에 CSS 클래스 이름이 중복되어도 새로운 이름이 입혀져 중복 및 관리의 위험성이 적고 CSS 네이밍 규칙이 간소화 된다. 다만 한 곳에서 모든 것을 작성하지 않기 때문에 별도로 많은 CSS 파일을 만들어 관리해야 하는 단점이 있다.

모듈화 된 CSS는 번들러를 통해 모든 CSS를 하나의 CSS 파일로 병합하거나, 자바스크립트 번들에 포함시킨다. 브라우저는 이 CSS를 로딩하고 적용한다.

### CSS-in-JS란?

> CSS-in-JS는 JavaScript 안에서 CSS 스타일을 작성하고 조작하는 방법을 의미한다.

CSS-in-JS는 JavaScript의 변수와 함수를 활용하여 동적인 스타일링을 가능하게 한다. 이는 애플리케이션의 상태에 따라 스타일이 바뀌어야 하는 경우에 특히 유용하다.

CSS-in-JS는 JavaScript 번들의 일부로 스타일을 로드한다. 이는 별도의 HTTP 요청 없이 스타일을 로드할 수 있음을 의미한다.

대부분의 CSS-in-JS 라이브러리는 브라우저에서 JavaScript를 실행하여 동적으로 style 태그를 생성하고, 이 태그에 스타일을 삽입한다.
