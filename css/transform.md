# transform

### transform이란 
좌표공간을 변형함으로써 일반적인 문서 흐름을 방해하지 않고 콘텐츠의 형태와 위치를 바꾸는 것을 말하며 여러 개의 CSS 속성을 조합해 구현합니다. 변형은 평면과 3D 공간에서의 회전, 확대, 이동, 비틀기를 포함한다.

### 주의 점
```  요소의 변환 효과
transform: 변환함수1 변환함수2 변환함수3 ...;
transform: 원근법 이동 크기 회전 기울임;
* 원근법 함수 perspective()는 제일 앞에 작성해야 한다
```

### 2D 변환 함수
- translate(x,y) 이동(x축, y축)
- translateX(x) 이동(x축)
- translateY(y) 이동(y축)
- scale(x,y) 크기(x축, y축)
- rotate(degree) 회전(각도)
- skewX(x) 기울임(x축)
- skewY(y) 기울임(y축)


### 3D 변환 함수


- perspective(n) 원근법(거리)
- 가까워질수록 왜곡이 심해진다.
- rotateX(x) 회전(x축)
- rotateY(y) 회전(y축)

<p align="center">
 <img src = "https://velog.velcdn.com/images/hyorimm/post/c58f6a1c-0c3b-48a4-93e9-a72e919a8b71/image.png">
</p>


### perspective 속성과 함수의 차이점
#### 속성

- 문법
perspective:600px;
- 적용 대상 - 관찰 대상의 부모
- 기준점 - perspective-origin

#### 함수
- 문법 transform:perspective(600px);
- 적용 대상 - 관찰 대상
- 기준점 - transform-origin

<p align="center">
 <img src = "https://velog.velcdn.com/images/hyorimm/post/0ba75768-1192-4ea3-976d-790e8c7780ca/image.png">
</p>

- backface-visibility <br>
-> visible 뒷면 보임<br>
-> hidden 뒷면 숨김