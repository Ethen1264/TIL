# React PDF Viewer

### PDF Viewer를 만들게 된 계기

SMS 학교 회의 도중 학생들이 올려둔 본인의 포트폴리오 PDF를 조회해야하는 페이지를 만들어야 하는 스프린트가 계획되었다. 이로인해 PDF Viewer를 만들어 보게 되었다.

### 사용된 라이브러리

![](https://velog.velcdn.com/images/ethen1264/post/4753c300-bc49-40b7-8853-3228fdf09e8e/image.png)

`React PDF Viewer` https://react-pdf-viewer.dev/docs/ 해당 라이브러리를 통해 제작하였다.
해당 라이브러리를 선택하게 된 이유는 여러 자료를 찾아봐도 `react-pdf`에 대한 자료만 나오게 되었는데 사람들이 많이 사용하는 라이브러리 보다 조금 다른 특색있는 라이브러리를 사용해보고 싶어 `React PDF Viewer`를 선택하게 되었다.

### 사용하기

```tsx
npm install pdfjs-dist@3.4.120
```

```tsx
npm install @react-pdf-viewer/core@3.12.0
```

위의 두 패키지를 설치를 하고 아래와 같이 사용한다.

#### PDF 파일을 state에 저장하는 로직

```tsx
  const [pdfFile, setPDFFile] = useState(null);
  const [viewPDF, setViewPdf] = useState(null);

  const fileType = ['application/pdf'];
  const handleChange = (e) => {
    let selectedFile = e.target.files[0];
    if (selectedFile) {
      if (selectedFile && fileType.includes(selectedFile.type)) {
        let reader = new FileReader();
        reader.readAsDataURL(selectedFile);
        reader.onload = (e) => {
          setPDFFile(e.target.result);
        };
      } else {
        setPDFFile(null);
      }
    } else {
      console.log('please select');
    }
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    if (pdfFile !== null) {
      setViewPdf(pdfFile);
    } else {
      setViewPdf(null);
    }
  };
  const newplugin = defaultLayoutPlugin();
  return (
    <S.Wrapper>
      <S.Container>
        <form onSubmit={handleSubmit}>
          <S.Input type="file" className="form-control" onChange={handleChange} />
          <S.Button type="submit" className="btn btn-success">
            PDF 확인하기
          </S.Button>
        </form>
```

#### state에 저장한 pdf를 화면에 랜더링 하는 로직

```tsx
<S.PDFContainer>
  <Worker workerUrl="https://unpkg.com/pdfjs-dist@3.11.174/build/pdf.worker.min.js">
    {/* {viewPDF ? <Viewer fileUrl={viewPDF} /> : <>NO PDF</>} */}
    {viewPDF ? <Viewer fileUrl={viewPDF} plugins={[newplugin]} /> : <>NO PDF</>}
  </Worker>
</S.PDFContainer>
```

> Viewer: PDF 파일을 보여주는 컴포넌트이다. fileUrl 속성에 보여줄 PDF 파일의 데이터 URL을 설정하고, plugins 속성에 사용할 플러그인을 지정할 수 있더ㅏ.
> defaultLayoutPlugin: PDF 뷰어에 기본 레이아웃 플러그인을 추가하여 기능을 확장한다. (pdf를 확대 축소 등 pdf를 조작할 수 있는 툴들을 생성하고 설정할 수 있다.)

### 참고 자료

https://www.youtube.com/watch?v=9eMFU3oV7cQ
