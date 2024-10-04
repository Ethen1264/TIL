# why use ManagingState

리액트에서 전역관리 상태 라이브러리가 필요한 이유는 애플리케이션의 규모가 커지고 복잡해질수록 컴포넌트간에 데이터 공유와 상태관리를 보다 편하게 사용하기 위해 사용한다. 물론 이러한 부분 뿐만 아닌 사용하는 여러 이유가 있다. 오늘은 이것을 알아볼려고 한다.

### 컴포넌트간 데이터 공유

여러 컴포넌트간 공통으로 사용되는 상태가 있다. 예를 들면 사용자 인증 정보, 로그인 상태, 언어, 테마, 설정 등 애플리케이션의 여러 곳에서 공유해야하는 데이터가 있을 때이다. 이러한 경우 상태관리라이브러리를 통해 공통적으로 사용할 수 있다.

### 상태의 일관성 유지

리액트는 단방향 데이터 흐름을 가지고 있으며 그 방향은 하향식으로 고정되어 있다. 중첩된 컴포넌트가 많은 경우 상태를 상위로 전달하는 것이 번거로울 수 있다. 전역 상태 관리를 통해서 여러 컴포넌트에서 동일한 상태에 접근하고 업데이트할 수 있으며 이를 통해 상태의 일관성을 유지할 수 있다.

### 애플리케이션의 복잡성 관리

대규모의 애플리케이션은 다양한 컴포넌트로 구성될 수 있다. 각 컴포넌트의 상태를 개별적으로 관리하는 것은 어렵기 때문에, 전역 상태 관리 라이브러리를 사용하는 방법을 사용할 수 있다. 애플리케이션의 복잡성을 줄이고 상태 관리를 효과적으로 처리할 수 있다.

### 컴포넌트간 분리

전역 상태 관리를 통해 컴포넌트 간에 데이터를 분리할 수 있다. 컴포넌트의 재사용성을 높이고 유지보수를 용이하게 만들 수 있다.

### 비동기 상태 관리

비동기 작업 (API 호출, 데이터 로딩 등)을 처리하는 경우, 전역 상태 관리를 사용하면 여러 컴포넌트에서 해당 상태에 접근하고 업데이트할 수 있다. 또한 비동기 작업이 완료된 후에도 상태를 적절하게 관리할 수 있다.