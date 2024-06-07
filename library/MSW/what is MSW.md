# what is MSW

### MSW란?

MSW(Mock Service Worker)는 서비스 워커(Service Worker)를 사용하여 네트워크 호출을 가로채는 API 모킹(mocking) 라이브러리이다. 즉 마치 백엔드 API인 척하면서 프론트엔드의 요청에 가짜 데이터를 응답해주는 녀석이라고 볼 수 있다.

### MSW의 특징

기존 API 모킹 라이브러리 대비 MSW의 가장 큰 강점은 모킹이 네트워크 단에서 일어나기 때문에 프론트엔드 코드를 실제 백엔드 API와 네트워크 통신하는 것과 크게 다르지 않게 작성할 수 있다. 즉 나중에 가짜 API를 실제 API로 대체하는 것이 쉽다는 뜻이며 그만큼 프론트엔드 프로젝트의 개발 생산성이 올라가는 것을 의미한다.