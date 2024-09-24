# reflow vs repaint

### 브라우저 렌더링 최적화

`브라우저 렌더링`은 측정 조건에 따라 `반복적으로 실행`이 된다.
그렇기 때문에 렌더링이 언제 발생하는지 알게되면 우리는 불필요한 렌더링을 막을 수 있다.

### 렌더링이 반복되는 경우

1. 자바스크립트에 이한 노드 추가 또는 삭제
2. 브라우저 창의 리사이징에 의한 뷰포트 크기 변경
3. HTML 요소의 레이아웃에 변경을 발생시키는 스타일 변경

위의 경우 Layout 계산과 Paint 과정이 재차 실행되어 리렌더링이 발생하게 된다.

이 과정에서 Layout 계산을 다시 수행하는 것을 `Reflow`, 픽셀을 렌더링하는 Paint 작업을 다시 하는 것을 `Repaint` 라고 한다.

### Reflow

- Dom 요소의 `위치와 크기를 다시 계산`하는 Layout 과정이다.
- 렌더링 트리를 다시 생성하므로 부하가 크고, 상위 엘리먼트가 변경되면 하위 엘리먼트에도 영향을 끼킨다.
- 예시
  - 노드의 추가, 제거
  - 위치 변경, 크기 변경, 폰트 변경, 윈도우 리사이징

#### 주의점

사실 `Reflow`의 개념만 보고 바로 알 수 있다. `Reflow`는 요소의 위치와 크기를 다시 계산하는 작업이기 때문에 `Reflow가 발생하면 Repaint까지 발생`한다. 즉 큰 비용이 발생한다.

- JS, CSS 파싱 -> 렌더 트리 구축 -> _Layout(Reflow) -> Paint(Repaint) -> 레이어 업데이트 -> Composite_
  위의 순서초롬 Reflow가 발생하면 Repaint와 Composite 과정을 모두 수행하게 된다.
  그렇기에 큰 비용이 발생한다.

### Repaint

- Layout 과정에는 영향을 미치지 않고 `변경된 요소를 화면에 그려줄 때` 발생한다.
- 예시
  - visibility, background-color, color
    만약 Repaint가 발생하면 Repaint와 Composite 과정만 거치게 되므로 Reflow 보다 상대적으로 훨씬 가벼운 작업이다.

### 결론

- Reflow: 위치와 크기를 계산하는 기하학적인 변화 즉 `Layout`을 담당
- Repaint: 기하학적인 변화 외의 `눈에 보여지는 부분`만 변경

### Reflow와 Repaint 최소화 하기

#### 1. 영향받는 노드 최소화하기 (position fixed, absolute)

- 상위 노드의 스타일을 변경하면 하위 노드에 모두 영향을 준다.
- 따라서 다른 엘리먼트 레이아웃에 영향을 주지 않는 fixed와 absolute 속성을 사용하면 비용을 줄일 수 있다.

#### 2. 숨겨진 엘리먼트 수정

- `display: none`의 경우 Reflow와 Repaint가 발생하지 않는다.
- 많는 수의 엘리먼트를 변경해야 할 경우, 숨겨진 상태에서 변경하고 다시 보여지도록 `display: none` 속성을 설정하여 레이아웃 발생을 최대한 줄일 수 있다.
- `visibility: hidden`의 경우 보이지 않기 때문에 `Repaint`는 일어나지 않지만 공간을 차지하기 때문에 Laout은 발생한다.

#### 3. transform, opacity 속성 사용하기

- 두 속서은 reflow와 repaint가 일어나지 않는 속성이다.
- left, right 대신 `transform` 속성을 사용한다.
- visibility, display 대신 `opacity` 속성을 사용하면 reflow, repaint 발생을 최소화 할 수 있다.

#### 4. 애니메이션 최적화

- 한 프레임의 처리는 16ms(60fps) 내로 완료되어야 끊기는 현상 없이 자연스럽게 처리된다.
- 자바스크립트에서 setTimeout을 이용하여 애니메이션을 구현한다면 이벤트 루프에 의해 딜레이가 생길 수 있고, 16ms 안에 실행하지 못한다면 해당 프레임은 유실된다.
- 이를 도와주는 것이 `requestAnimationFrame()` 메서드 이다.
  - 장점: 지연 및 블로킹 없이 일정한 간격으로 애니메이션을 수행
  - 브라우저 프레임 속도 (60fps)에 맞춰 애니메이션을 실행
  - 페이지가 비활성 상태일 때 렌더링을 중지한다. -> CPU의 리소스와 배터리 수명을 낭비 하지 않음
  - 이와 달리 setTimeout은 백그라운드 상태일 때도 계속 실행