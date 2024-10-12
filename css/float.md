# float

float은 css의 레이아웃을 잡는 개념중에 하나로 주로 이미지와 텍스트의 주위를 감싸는데 사용된다.
![](https://velog.velcdn.com/images%2Fshin6403%2Fpost%2Facedf7c8-e954-43b7-9ccc-abaf7b6b61d0%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-10-20%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.26.37.png)

### float속성

- none: 기본 속성, 요소를 띄우지 않는다.
- left: 요소를 왼쪽으로 띄운다.
- right: 요소를 오른쪽으로 띄운다.
- inherit: 부모의 속성을 상속 받는다.

float에는 위와 같은 속성이 있는데

```tsx
 <img style="float:left" width="200px" height="200px" src="eagle.jpg" />
 <div>float:left 왼쪽 속성 테스트 입니다. 보이는 것처럼 사진이 왼쪽으로 이동해있고 글이 오른쪽으로 오는것을 알 수 있습니다. 말을 길게 써야 글이 물 흐르듯이 써지는걸 보여야할텐데요.</div>
```

![](https://velog.velcdn.com/images%2Fshin6403%2Fpost%2Fdc3411a9-9c55-46bc-8380-cd614fa22362%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-10-20%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.55.38.png)
위와 같이 사용한다.

### clear 속성

위의 float처럼 사진 주면에 텍스트가 물 흐르듯 배치되는 것을 헤제하기 위해 clear속성이 사용된다.

- none: 아무런 해제를 하지 않는다.
- left: float:left를 해제한다.
- right: float:right를 해제한다.
- both: 모든 float(left,right)를 해제한다.
- inherit: 부모의 속성을 상속 받는다.

```tsx
<img style="float:left" width="200px" height="200px" src="eagle.jpg" />
<div style="clear:both;"class="eagle">clear:both 속성 테스트 입니다. 보이는 것처럼 사진에 있던 float 속성이 해제되고 다시 사진 밑으로 글이 배치되는걸 보고 있습니다.</div>
```

![](https://velog.velcdn.com/images%2Fshin6403%2Fpost%2F3a61d319-7308-419a-9313-6820c19f8471%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-10-20%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%206.08.59.png)

clear 속성이 지정된 영역 이후에는 더이상 float가 작동하지 않는다.

### clearfix 핵

float 속성을 적용한 이미지의 크기가 커서, 이미지를 담고 있는 엘리먼트 영역을 침범해서 배치되는 경우가 있다.

![](https://velog.velcdn.com/images%2Fshin6403%2Fpost%2F34e1205f-2ba8-49f9-a252-538c59b7ae6a%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-10-20%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%206.21.15.png)

이런 문제를 해결하는 방법이 한 가지 있는데, 이를 clearfix 핵이라고 한다.

```tsx
.eagle {
  overflow: auto;
}

<div class="eagle">
    <img style="float:left" width="200px" height="200px" src="eagle.jpg" />
    <div>이런.. 이미지가 텍스트 요소보다 더 커서 컨테이너 바깥으로 넘쳤네요!</div>
</div>
```

![](https://velog.velcdn.com/images%2Fshin6403%2Fpost%2F9df63ae2-07e1-493c-91d3-103ae2e5cf72%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-10-20%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.41.59.png)
