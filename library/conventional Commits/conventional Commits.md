# conventional Commits

Conventional Commits는 명확한 커밋 히스토리 관리를 위한 메세지 작성 규칙에 대해 제안하고 있다. 이러한 conventional Commits을 사용하면 Semantic Versioning 관리에도 효과적이다.

### structure

![alt text](../img/conventional%20Commits.png)

커밋 메세지의 헤더는 필수적으로 작성되어야 하며, 작업 내용의 특징과 요약된 내용을 type과 description으로 명시해야 한다. 그 외에 적용 범위나 본문과 꼬리말은 선택적으로 작성하면 되고, Semantic Versioning에도 영향을 주지 않는다.

### type

커밋에 기록된 작업들의 성격이 무엇인지 알려주는 역할을 한다. 대표적으로 fix와 feat이 있으며, 앵귤러 컨벤션에서는 `build`, `chore`, `ci`, `docs`, `style`, `refactor`, `perf`, `test` 등의 타입을 사용할 것을 권고하고 있다.

> fix : 버그 수정과 관련된 커밋 타입. Semantic Versioning의 Patch와 관련
> feat : 새로운 기능에 대한 커밋 타입. Semantic Versioning의 Minor와 관련
> build : 빌드 관련 파일 수정에 대한 커밋 타입
> chore : 분류하기 어려운 자잘한 수정에 대한 커밋 타입
> ci : CI 관련 수정에 대한 커밋 타입
> docs : Documentation 수정에 대한 커밋 타입
> style : 코드 의미에 영향을 주지 않는 수정에 대한 커밋 타입
> refactor : 코드 리팩토링에 대한 커밋 타입
> test : 테스트 코드 수정에 대한 커밋 타입

### scope

해당 커밋이 어떤 범위의 수정 사항인지 부가적인 설명을 하는 부분이다. 협업을 할 때에 작업을 분담해서 진행하기 때문에 범위에 대한 정보를 포함해서 커밋 메세지를 작업한다면 서로의 업무를 파악하는데 도움이 된다.

### description

해당 커밋의 작업 내용을 요약해서 적어야 한다. Add product detail information get method와 같이 현재형 동사로 적는 것이 일반적이다.

### body

type과 description으로 요약해서 전달하기 어려운 세부적인 내용에 대해서 적는 부분이다. Semantic Versioning에서 Major에 대한 수정이 일어난다면 body를 작성하는 것이 필수적으로 요구된다.
