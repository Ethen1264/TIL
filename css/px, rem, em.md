# px, rem, em

### 단위를 사용하게 된 배경

반응형 웹은 크기와 넓이에 따가 컴포넌트들의 크기도 각기 변해야한다. 그떄 절대단위를 사용한다면 이러한 컴포넌트의 크기 변화를 볼 수 없고 상대적 단위를 사용해야 한다.

### 상대적 단위와 절대적 단위

상대적단위는 크기가 고정되어 있지 않고 현재 상태에 따가 크기가 변하는 것을 말한다. 대표적으로 **em, rem, %, vw, vh**등이 있다.

절대적 단위는 어떤 상황이던 고정되어 있는 상태의 단위이다. 절대단위에는 **px**단위가 가장 많이 쓰인다.


### PX

px는 절대 크기의 단위로 이 값은 한번 정의하면 변하지 않는다.

### em

em은 해당 단위가 사용되고 있는 요소의 font-size를 기준으로 px로 바뀌어 화면에 표시된다. 같은 엘리먼트에 설정된 폰트 크기 값이 없을 경우에는 상위 요소의 폰트 사이즈가 기준이 된다.


``` css
.container {
  font-size: 16px;
}

.container .div {
  font-size: 20px;
  width: 2em; /* 40px */
}
```

``` css
.container {
  font-size: 16px;
}

.container .div {
  width: 2em; /* 32px */
}
```

### rem

최상위 엘리먼트에서 지정된 font-size의 값을 기준으로 변환된다. HTML에서 최상위 요소는 html태그이기 떄문에 html 요소의 font-size 속성값이 기준이 된다. 만약 별도의 font-size를 설정하지 않았을 경우에는 각 브라우저에서 기본적으로 설정된 값을 상속 받는다. 보통 16px로 정의되어 있다.

``` css
.html {
  font-size: 25px;
}

.container .div {
  font-size: 20px;
  width: 2rem; /* 50px */
}
```

``` css

.container .div {
  font-size: 20px;
  width: 2rem; /* 32px */
}
```
