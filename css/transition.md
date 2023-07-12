# trandition 

### trandition이란?
CSS 속성을 변경할 때 애니메이션 속도를 조절하는 방법을 제공하는 속성이다.

### trandition 속성의 종류
- transition-property
- transition-duration
- transition-delay
- transition-timing-function

### transition-property 속성
```전환 효과를 적용할 대상 속성 지정```

|속성 값|설명|
|:---:|:---:|
|none|전환 효과 속성을 지정하지 않습니다|
|all|모든 속성을 전환 효과 대상으로 지정함|

### transition-duration 속성
```전환 효과의 지속 시간을 설정하는데 사용``` <br>
여러 속성을 쉼표로 구분해 전환효과를 지정 시 property와 duration 속성을 각각 지정 가능<br>
-> ```전환 효과를 지정하려면 이 두 속성은 반드시 사용 해야 함```


### transition-delay 속성
```전환 효과의 발생을 지연시킬 수 있음```

```css
.red-box{
	...
    transition-delay:1s;
}
```

### transition 속성으로 한번에 지정

``` css
transition:<property>, <duration>, <timing-function>, <delay>;
transition-property:width;
transition-duration:1s
transition-timing-function:ease-in;
transition-delay:1s;

transition:width, 1s, ease-in, 1s;
```