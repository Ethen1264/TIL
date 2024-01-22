# 내가 좋아하는 css 신기능 

- Container query
- support
- :is()

## Container query (@container)

css로 기존의 반응형을 만들기 위해선 ```@media``` 즉 ```media query```를 사용해 왔다. 이 ```@media```는 viewport를 기준으로 속성이 변한다는 특징이 있었는데 화면 내부의 특정 영역 안에 위치할 디자인을 만드려면 본문과 완전히 같은 디자인을 적용하더라도 본문과 구분하여 따로 관리해야하는 불편함이 있었다. 하지만 ```Container query``` 즉 ```@container```는 viewport대신 영역을 감싼 container를 기준으로 적용된다.

```css
.main-container  {
  container-type: inline-size;  // 새롭게 추가됨
}
.h1 {
  font-size: 30px
}

@container (max-width: 800px) {
  .h1 {
  font-size: 20px
}
```

부모 컨테이너가 800px이하이면 h1의 폰트 사이즈가 30px에서 20px로 줄어들게 된다.

### container-type는 뭘까?
```size```, ```inline-size```, ```normal```의 세 가지 값을 가질 수 있다. ```normal```은 해당 값이 부여된 ```htmlelement```를 ```container```에서 제외한다. ```size```는 ```container를``` 블록 레벨로 적용하기 때문에 ```height```값이 조건에 해당할 때에도 ```container query```를 적용한다.

```inline-size```는 인라인 요소를 기준으로 컨테이너를 적용하기 때문에 ```width```값에 따라 ```container query```를 적용할 수 있다. 

### cqw, cqv
viewport의 vw,vh처럼 container의 너비와 높이를 기준으로 하는 단위이다. container query의 기준점을 정할 때 상대단위로 이용할 수 있다.

## @support

```@support```는 쉽게 말해서 A스타일을 지원하는 브라우저에는 A스타일을 적용을 하고 만약 A스타일을 지원하지 않다면 B스타일을 적용하는 기능이다. 

```css
header {
	display: flex;
}

@supports (display: grid) {
	header {
    	display: grid;
    }
}
```

그럼 위의 코드로 예시를 들자면 만약 C브라우저에서 ```display: grid```라는 스타일 속성을 지원을 한다면 ```display: grid```를 적용을하고 만약 지원을 하지 않다면 ```display: flex```를 적용하는 기능이다.

### Support에 not과 and와 or을??
제목에서 본 것 처럼 ```support```는 not, and, or을 적용할 수 있다.

#### not
```css
@supports not (display: grid) {
	.old-browser-alert {
    	display: flex;
    }
}
``` 
만약 브라우저에서 grid라는 속성을 지원하지 않는다면 alert으로 display: flex라는 경고창이 나타나도록 되어있다.

not과 not을 두번써서 not을 한번 더 부정하는 방법도 있다.

#### and

```css
@supports not ((display: flex) and (display: grid)) {
	.old-browser-alert {
    	display: block;
    }
}
```

브라우저가 ```display: flex```와 ```display: grid```를 둘 다 지원하는지 확인하고, 하나라도 지원하지 않다면 유저에게 경고를 표시한다.

#### or

```css
@supports not ((display: flex) or (display: grid)) {
	.old-browser-alert {
    	display: block;
    }
}
```
브라우저가 ```display: flex```와 ```display: grid```가 지원하는지 확인하고, 둘 다 지원하지 않다면(하나라도 지원하는 경고가 출력이 안됨) 유저에게 경고를 표시한다,

## :is()

보통 css로 style을 주다보면 class가 여러게 섞여 한번에 적용되는 경우가 있다. 나는 이렇게 지저분한게 정말 싫었었기 때문에 이 기능을 보자마자 엄청 놀랐다.

예를 들어서

```css
h1 {
	font-size: 26px;
}

section h1,
div h1,
nav h1,
footer h1,
article h1 {
	font-size: 16px;
}
```

전에는 이렇듯 ```section h1```, ```div h1```, ```nav h1```, ```footer h1```, ```article h1``` 이렇게 많은 id와 class를 한번에 적어줘야 했다. 하지만 :is()를 사용하면 

```css
h1 {
	font-size: 26px;
}

:is (section, nav, footer, article, div) h1 {
	font-size: 16px;
}
```

이렇게 한번에 줄여서 사용할 수 있다.