# css flex

## flex 속성들은 크게 두가지로 나눌 수 있다.
- 컨테이너에 적용하는 속성
- 아이템에 적용하는 속성

<hr>	

첫번째로 컨테이너에 적용하는 속성에는 크게 아래와 같은 종류가 있다.
- display: flex;
- flex-direction
- flex-wrap
- flex-flow
- justify-content
- align-items
- align-content
<hr>
첫번째로 display: flex 속성은 아이템들이 세로가 아닌 가로 뱡향으로 정렬되게 설정이 되게 하며 block 처럼 한 줄의 공간을 차지하는 것이 아닌 자기가 있는 글자 공간 크기 만큼만 차지한다. 또 아이템이 배치가 된 방향을 메인축 이라고 하고 메인축에 수직인 방향을 수직축 이라고 부른다.
<hr>
두번쨰로 flex-direction은 아이템들이 배치가 되는 축의 방향을 지정하는 속성 입니다. 

```css
.container {
	flex-direction: row;      /* 아이템들을 가로 방향으로 배치한다 */
	flex-direction: column;   /* 아이템들을 세로 방향으로 배치한다 */
	flex-direction: row-reverse;  /* 아이템들을 가로의 역 방향으로 배치한다 */
	flex-direction: column-reverse; /* 아이템들을 세로의 역 방향으로 배치한다*/ 
}
```
<hr>
세번째로 flex-wrap은 컨테이너가 더 이상 아이템들을 한 줄에 담을 여유 공간이 없을 때 아이템의 줄바꿈 방식을 결정하는 속성이다.

```css
.container {
	flex-wrap: nowrap;        /*아이템을 둘 공간이 없다면 가로를 삐져 나감*/
	flex-wrap: wrap;          /*아이템을 둘 공간이 없다면 줄바꿈이 진행됨*/
	flex-wrap: wrap-reverse;  /*아이템을 둘 공간이 없다면 역 방향으로 줄바꿈됨*/
}   
```
<hr>
네번째로 flex-flow는 flex-direction과 flex-wrap을 한꺼번에 지정할 수 있는 단축 속성이다. 

```css
.container {
	flex-flow: row wrap;
	/* flex-direction: row; */
	/* flex-wrap: wrap; */
}
```
<hr>
다섯번째로 justify-content는 메인축 방향으로 아이템을 정렬하는 속성이다.

```css
.container {
	justify-content: flex-start;		/*아이템들을 시작점으로 정렬한다.*/
	justify-content: flex-end; 			/*아이템을 끝 지점으로 정렬한다*/
	justify-content: center;				/*아이템을 가운데로 정렬한다*/
	justify-content: space-between;	/*아이템들 사이에 일정한 간격을 준다*/
	justify-content: space-around;	/*아이템들의 둘레에 일정한 간격을 준다*/
	justify-content: space-evenly;	/*아이템들의 사이와 양 끝에 균일한 간격을 준다.*/
}
```
<hr>
여섯번째로 align-items는 수직으로 아이템을 정렬하는 속성이다.

```css
.container {
	align-items: stretch;			/*아이템들을 수직 방향으로 늘린다.*/
	align-items: flex-start;	/*아이템들을 시작 지점으로 보낸다.*/
	align-items: flex-end;		/*아이템을 끝 지점으로 보낸다.*/
	align-items: center;			/*아이템을 중앙으로 보낸다*/
	align-items: baseline; 		/*아이템의 하단을 수평으로 정렬한댜.*/
}
```
<hr>
일곱번째로 align-content는 아이템들의 행이 2줄 이상 되었을 때의 수직축 방향 정렬을 결정하는 속성이다.

```css
.container {
	align-content: stretch;				/*정렬 컨테이너의 교차축 방향을 가득 채움*/
	align-content: flex-start;		/*플렉스 항목을 한 덩어리로 뭉치고, 정렬 컨테이너의 시작점 모서리에 배치함*/	
	align-content: flex-end;			/*플렉스 항목을 한 덩어리로 뭉치고, 정렬 컨테이너 끝점 모서리에 배치합니다.*/
	align-content: center;				/*정렬 컨테이너 교차축의 중앙에 배치한다.*/
	align-content: space-between;	/*첫 항목은 정렬 컨테이너 교차축의 시작점에, 마지막 항목은 정렬 컨테이너 교차축의 종료점에 배치한다.*/
	align-content: space-around;	/*첫 항목 이전 여백과 마지막 항목 이후 여백은 각 항목간 거리의 절반이 된다.*/
	align-content: space-evenly;	/*첫 항목 이전 여백, 마지막 항목 이후 여백이 모두 같아진다.*/
}
```
<hr>
두번째로 아이템에 적용하는 속성에는 크게 아래와 같은 종류가 있다.

- flex-basis
- flex-grow
- flex-shrink
- align-self
- order
- z-index
<hr>

첫번째로 flex-basis는 flex 아이템의 기본 크기를 설정한다.
```css
.item {
	flex-basis: auto; /* 기본값 */
	flex-basis: 0;
	flex-basis: 50%;
	flex-basis: 300px;
	flex-basis: 10rem;
	flex-basis: content;
}
```
<hr>
두번째로 flex-grow에 들어가는 숫자의 의미는, 아이템들의 flex-basis를 제외한 여백 부분을 flex-grow에 지정된 숫자의 비율로 나누어 가진다.

```css
.item {
	flex-grow: 1;
	/* flex-grow: 0; */ /* 기본값 */
}
```
이런식으로 지정하면 아이템들의 비율이 1이 된다.
<br>
또 다른 방법으론 

```css
.item:nth-child(1) { flex-grow: 1; }
.item:nth-child(2) { flex-grow: 2; }
.item:nth-child(3) { flex-grow: 1; }
```
이런 식으로 지정해서 1:2:1 바율로 지정할 수 있다.
<hr>

세번째 flex-shrink는 flex-grow와 쌍을 이루는 속성으로, 아이템이 flex-basis의 값보다 작아질 수 있는지를 결정한다. 또 flex-shrink를 0으로 세팅하면 아이템의 크기가 flex-basis보다 작아지지 않기 때문에 고정폭의 컬럼을 쉽게 만들 수 있고 고정 크기는 width로 설정할 수 있다.

```css
.container {
	display: flex;
}
.item:nth-child(1) {
	flex-shrink: 0;
	width: 100px;
}
.item:nth-child(2) {
	flex-grow: 1;
}
```
<hr>
네번째 align-self는 해당 아이템의 수직축 방향 정렬이다.

```css
.item {
	align-self: auto;				/*요소의 정렬 상태를 기본으로 설정한다.*/
	align-self: stretch;		/*요소의 가로 영역 값을 최대로 설정한다*/
	align-self: flex-start; /*요소의 정렬을 시작점으로 설정한다.*/
	align-self: flex-end;		/*요소의 정렬을 끝점으로 설정한다.*/
	align-self: center;			/*요소의 정렬을 가운데로 설정한다.*/
	align-self: baseline;		/*요소의 정렬을 폰트를 기준으로 설정한다.*/
}
```

<hr>
다섯번째 order는 각 아이템들의 시각적 나열 순서를 결정하는 속성이다.

```css
.item:nth-child(1) { order: 3; } /* A */
.item:nth-child(2) { order: 1; } /* B */
.item:nth-child(3) { order: 2; } /* C */
```
이런식으로 설정하면 B C A 순으로 나열된다.

<hr>
z-index로 Z축 정렬을 할 수 있고 숫자가 클 수록 위로 올라온다.

``` css
.item:nth-child(2) {
	z-index: 1;
	transform: scale(2);
}
/*z-index를 설정 안하면 0이므로, 1만 설정해도 나머지 아이템을 보다 위로 올라온다 */
```