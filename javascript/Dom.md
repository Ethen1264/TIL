# Dom

### Dom이란?

문서 객체 모델은 html, xml 문서의 프로그래밍 interface이다.
Dom은 nodes와 object로 문서를 표현한다. 이들은 웹페이지들을 스크립트 또는 프로그래밍 언어들에서 사용할 수 있게 연결하는 역할을 한다.

자바스크립트에서 html을 가져오거나 수정하는 역할을 한다.

### id를 사용해서 dom 찾기

**document.getElementById()**

**document.querySelector()**

```tsx
<div>
    <label for="userId">사용자 ID</label>
    <input type="text" name="" id="userId" class="form-control" />
</div>

<script>
    const userId = document.getElementById("userId");
    console.log(userId); //<input type="text" name="" id="userId" class="form-control" />

    const userId2 = document.querySelector("#userId");
    console.log(userId2); //<input type="text" name="" id="userId" class="form-control" />

    //작성한 값 가져오기
    console.log(document.querySelector("#userId").value);
</script>
```

### 태그명을 사용해서 dom 찾기

**document.getElementsByTagName()**

**document.querySelectorAll()**

```tsx
<div>
    <label for="userId">사용자 ID</label>
    <input type="text" name="" id="userId" class="form-control" />
</div>

<script>
	const label = document.getElementsByTagName("label");
    console.log(label); //label 태그가 있는 html 요소를 배열로 리턴

    const label2 = document.querySelectorAll("label");
    console.log(label2); //label 태그가 있는 html 요소를 배열로 리턴

    //작성한 값 가져오기
    console.log(document.querySelectorAll("label").value);
</script>
```

### 클래스명을 사용해서 DOM 요소 찾기

**document.getElementsByClassName()**

**document.querySelectorAll()**

```tsx
    <label for="userId">사용자 ID</label>
    <input type="text" name="" id="userId" class="form-control" />
</div>

<div>
    <label for="userPass">비밀번호</label>
    <input type="text" name="" id="userPass" class="form-control" />
</div>

<script>
    const classElement = document.getElementsByClassName("form-control");
    console.log(classElement); //해당 클래스명이 적힌 html 요소를 배열로 리턴

    const classElement2 = document.querySelectorAll("form-control");
    console.log(classElement2); //해당 클래스명이 적힌 html 요소를 배열로 리턴

    //작성한 값 가져오기
    console.log(document.querySelectorAll("form-control").value);
</script>
```

### name 속성을 사용해서 DOM 요소 찾기

**document.getElementsByName()**

**document.querySelectorAll()**

```tsx
 <div>
    <input type="checkbox" name="chk_lang" id="html" value="HTML" />
    <label for="html">HTML</label>
    <input type="checkbox" name="chk_lang" id="css" value="CSS" />
    <label for="css">CSS</label>
    <input type="checkbox" name="chk_lang" id="js" value="JS" />
    <label for="js">JS</label>
</div>

<script>
	const chkLangs = document.getElementsByName("chk_lang");
    let checkedValue = [];

    //체크된 값만 저장하고 싶다면
    for (const lang of chkLangs) {
    	if (lang.checked) {
        	checkedValue.push(lang.value);
        }
    }

    //querySelectorAll 을 이용
    const values = document.querySelectoAll("[name=chk_lang]");

    //querySelectorAll 을 이용해서 체크된 값만 저장하고 싶다면
    const checkedValue2 = document.querySelectoAll("[name=chk_lang]:checked");
</script>
```
