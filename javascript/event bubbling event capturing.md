## 이벤트 버블링 
- 이벤트 버블링의 원리??
- 이벤트 버블링을 막는 법 #1
- 이벤트 버블링을 막는 법 #2
- 이벤트 버블링을 막아야 할까?

### 이벤트 버블링의 원리
이벤트 버블링은 효과(ex onclick)가 발생된 본인부터 부모 태그들을 거처 window 까지 이벤트가 올라가는 것을 말합니다. 

![](https://velog.velcdn.com/images/ethen1264/post/6311f77c-5720-4e6b-9840-fbfdc3e284ad/image.png)

예시로 이러한 그림이 있다고 할때 파란 색을 클릭하면 1이 alert되고 초록을 클릭하면 2가 빨강을 클릭하면 3이 alert된다고 하자. 그때 파란색을 클릭하면 본인인 1 alert가 실행되고 그 아래에 있던 초록의 2 alert이 실행되며 또 그 아래에 있는 빨강의 3 alert가 실행이 된다. 

### 이벤트 버블링을 막는 법 #1
**event.stopPropagation()** 을 이용하여 강제로 중단 시키는 방법이 있다. 하지만 **event.stopPropagation()** 은 위쪽으로 일어나는 버블링은 막아주지만, 다른 핸들러들이 동작하는 건 막지 못한다.

### 이벤트 버블링을 막는 법 #2
버블링을 멈추는 방법이 하나가 더 있다. 바로 **event.stopImmediatePropagation()** 이다. 하지만 이 **event.stopImmediatePropagation()** 은 버블링만을 멈추는 것이 아니라 요소에 포함되어 있는 이벤트들이 모두 정지된다.

### 사용해야 할까?
보통은 특정한 상황이 있지 않고선 막지 않는다. 이벤트 버블링을 막으면 추후에 문제가 일어날 수 있기 때문이다.

## 이벤트 캡처링 
- 이벤트 캡처링이란?
- 이벤트 캡처링의 사용성
- 이벤트 캡처링을 적용하는 법

### 이벤트 캡처링이란?
이벤트 캡처링은 이벤트 버블링과 반대로 window를 시작으로 이벤트가 발생한 곳 까지 이벤트를 전파한다.

### 이벤트 캡처링의 사용성 
이벤트 캡처링은 거의 쓰지 않는다.

### 이벤트 캡처링을 적용하는 법

```js
element.addEventListener(..., {capture: true})
// 또는
element.addEventListener(..., true)
```