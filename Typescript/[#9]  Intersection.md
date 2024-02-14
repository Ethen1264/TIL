# [#9] Intersection

### 인터섹션 타입이 없다면?

```ts
type TestProgrammer = { favoriteLanguage: string; favoriteEquipment: string };
const AhnHeejong: BeerLovingProgrammer = {
  favoriteLanguage: 'TypeScript',
  favoriteEquipment: 'Imperial Stout',
};
```

하지만 이런 접근은 코드 복사–붙여넣기와 동일하게 변화에 취약하다는 단점을 갖는다.
이런 비효율을 피하고 변화에 유연하게 대응하기 위해선 이미 존재하는 여러 타입을 모두 만족하는 타입을 표현하기 위한 수단이 필요하다. 인터섹션 타입은 바로 그걸 가능케 한다.

### 문법

여러 타입을 앰퍼샌드(&) 기호로 이어서 인터섹션 타입을 나타낼 수 있다.

```ts
type TestProgrammer = Programmar & Test;
```

A & B 타입의 값은 A 타입에도, B 타입에도 할당 가능해야 한다. 만약 A와 B 모두 객체 타입이라면 A & B 타입의 객체는 A와 B 타입 각각에 정의된 속성 모두를 가져야 한다.

```ts
type Test = string & number;
```

문자열인 동시에 숫자인 값은 존재하지 않기에 Intersection는 존재하지 않는다.
