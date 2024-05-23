# dayjs

### dayjs란?

Javascript에서는 Date객체를 외에도 시간과 날짜를 편리하게 관리할 수 있는 라이브러리이다. 이러한 dayjs 외에도 Momentjs도 존제 하지만 더 이상 업데이트 되지 않는다는 문제와 용량이 크다는 문제로 최근엔 dayjs를 많이 사용한다.

### 설치

```
yarn add dayjs
```

### 객체 생성

dayjs()를 통해 현재 날짜를 기준으로 객체를 생성하거나 ()안에 특정 날짜를 기준으로 생성할 수 있다.

```tsx
// 현재 날짜 객체 생성
dayjs();

// 지정한 날짜 객체 생성
dayjs('2024-05-23');
dayjs('2022-05-23 15:30:00');
```

### 날짜 형태 지정(format())

생성한 객체에 format() 함수를 활용하여 원하는 형태로 날짜 문자열을 변경할 수 있다.

```tsx
let date = dayjs('2022-12-01 10:30:25');

date.format();
date.format('YY-MM-DD'); // 24-05-23
date.format('DD/MM/YY'); // 23/05/24
date.format('YYYY.MM.DD HH:mm:ss'); // 2024.05.23 15:30:00
```

### 날짜 가져오기/수정하기(get/set)

#### 원하는 값 가져오기(get)

```tsx
let now = dayjs();

now.format();

// 년
now.get('year');
now.get('y');

// 월
now.get('month');
now.get('M');

// 일
now.get('date');
now.get('D');

// 요일 (일요일 : 0, 토요일 : 6)
now.get('day');
now.get('d');

// 시
now.get('hour');
now.get('h');

// 분
now.get('minute');
now.get('m');

// 초
now.get('second');
now.get('s');

// 밀리초
now.get('millisecond');
now.get('ms');
```

#### 원하는 값 넣기(set)

```tsx
let date = dayjs('2022-12-01 17:00:00');

date.format(); // 2022-12-01T17:00:00+09:00

date.set('year', 2023).format(); // 2023-12-01T17:00:00+09:00
date.set('y', 2023).format(); // 2023-12-01T10:17:00+00:00

date.set('month', 11).format(); // 2022-11-01T17:00:00+09:00
date.set('M', 11).format(); // 2022-11-01T17:00:00+09:00

date.set('date', 25).format(); // 2022-12-25T17:00:00+09:00
date.set('D', 25).format(); // 2022-12-25T17:00:00+09:00

date.set('day', 5).format(); // 2022-12-05T17:00:00+09:00
date.set('day', 5).format('dddd'); // Friday
date.set('d', 5).format(); // 2022-12-05T17:00:00+09:00
date.set('d', 5).format('dddd'); // Friday

date.set('hour', 15).format(); // 2022-12-01T15:00:00+09:00
date.set('h', 15).format(); // 2022-12-01T15:00:00+09:00

date.set('minute', 45).format(); // 2022-12-01T17:45:0009:00
date.set('m', 45).format(); // 2022-12-01T17:45:00+09:00

date.set('second', 10).format(); // 2022-12-01T17:00:10+09:00
date.set('s', 10).format(); // 2022-12-01T17:00:10+09:00
```

#### 날짜 더하기/빼기(add/subtract)

생성한 객체에서 원하는 만큼의 날짜를 더하고 뺄 수 있으며 첫번째 숫자는 더하고 빼는 수, 두번째 문자열은 단위를 나타낸다.

```tsx
// 년도
dayjs().add(1, 'year');
dayjs().subtract(1, 'year');

// 월
dayjs().add(1, 'month');
dayjs().subtract(1, 'month');

// 일
dayjs().add(1, 'day');
dayjs().subtract(1, 'day');

// 시간
dayjs().add(1, 'hour');
dayjs().subtract(1, 'hour');

// 분
dayjs().add(1, 'minute');
dayjs().subtract(1, 'minute');

// 초
dayjs().add(1, 'second');
dayjs().subtract(1, 'second');
```

#### 타임스탬프로 변환

valueOf() 함수를 통해 원하는 format으로 넣은 날짜를 타임스탬프로 변환할 수 있으며, dayjs()에 타임스탬프를 넣을 경우 설정한 format에 따라 다시 날짜로 다시 변환할 수 있다.

```tsx
dayjs(1669820400000).format(); // 2022-12-01T00:00:00+09:00
dayjs('2022-12-01').valueOf(); // 1669820400000
```

#### 날짜/시간 차이 구하기

주어진 날짜간에 차이를 원하는 단위로 얻을 수 있으며 세번째 인자로 true를 넣을 경우 소수점 단위까지 표시된다.

```tsx
const date1 = dayjs('2022-12-01 12:30:25.123');
const date2 = dayjs('2021-10-24 13:23:50.456');

date1.format('YYYY-MM-DD HH:mm:ss.SSS'); // 2022-12-01 12:30:25.123
date2.format('YYYY-MM-DD HH:mm:ss.SSS'); // 2021-10-24 13:23:50.456

date1.diff(date2); // 34815994667

date1.diff(date2, 'year'); // 1
date1.diff(date2, 'y'); // 1
date1.diff(date2, 'y', true); // 1.1047389818237257

date1.diff(date2, 'month'); // 13
date1.diff(date2, 'M'); // 13
date1.diff(date2, 'M', true); // 13.256867781884708

date1.diff(date2, 'week'); // 57
date1.diff(date2, 'w'); // 57
date1.diff(date2, 'w', true); // 57.566128748346564

date1.diff(date2, 'day'); // 402
date1.diff(date2, 'd'); // 402
date1.diff(date2, 'd', true); // 402.9629012384259

date1.diff(date2, 'hour'); // 9671
date1.diff(date2, 'h'); // 9671
date1.diff(date2, 'h', true); // 9671.109629722223

date1.diff(date2, 'minute'); // 580266
date1.diff(date2, 'm'); // 580266
date1.diff(date2, 'm', true); // 580266.5777833334

date1.diff(date2, 'second'); // 34815994
date1.diff(date2, 's'); // 34815994
date1.diff(date2, 's', true); // 34815994.667

date1.diff(date2, 'millisecond'); // 34815994667
date1.diff(date2, 'ms'); // 34815994667
date1.diff(date2, 'ms', true); // 34815994667
```
