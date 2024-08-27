# string

### String.prototype.charAt(number) : string

인수로 전달한 index를 사용하여 index에 해당하는 위치의 문자를 반환한다.

index는 0 ~ (문자열 길이 - 1) 사이의 정수이다. 지정한 index가 문자열의 범위(0 ~ (문자열 길이 - 1))를 벗어난 경우 빈문자열을 반환한다.

```tsx
const str = 'Hello';

console.log(str.charAt(0)); // H
console.log(str.charAt(1)); // e
console.log(str.charAt(2)); // l
console.log(str.charAt(3)); // l
console.log(str.charAt(4)); // o

// 지정한 index가 범위(0 ~ str.length-1)를 벗어난 경우 빈문자열을 반환한다.
console.log(str.charAt(5)); // ''
```

### String.prototype.indexOf(searchstring, fromIndex) : numbe

인수로 전달한 문자 또는 문자열을 대상 문자열에서 검색하여 처음 발견된 곳의 index를 반환한다.

`발견하지 못한 경우 -1을 반환한다.`

```tsx
const str = 'Hello World';

console.log(str.indexOf('l')); // 2
console.log(str.indexOf('or')); // 7
console.log(str.indexOf('or', 8)); // -1
```

### String.prototype.lastIndexOf(searchString, fromIndex) : number

인수로 전달한 문자 또는 문자열을 대상 문자열에 검색하여 마지막으로 발견된 곳의 index를 반환한다. 발견하지 못한 경우 -1을 반환한다.

2번째 인수(fromIndex)가 전달되면 검색 시작 위치를 fromIndex으로 이동하여 역방향으로 검색을 시작한다 이때 검색 범위는 0 ~ fromIndex이며 반환값을 indexOf 메소드와 동일하게 발견된 곳의 index이다.

```tsx
const str = 'Hello World';

console.log(str.lastIndexOf('World')); // 6
console.log(str.lastIndexOf('l')); // 9
console.log(str.lastIndexOf('o', 5)); // 4
console.log(str.lastIndexOf('o', 8)); // 7
console.log(str.lastIndexOf('l', 10)); // 9

console.log(str.lastIndexOf('H', 0)); // 0
console.log(str.lastIndexOf('W', 5)); // -1
console.log(str.lastIndexOf('x', 8)); // -1
```

### String.prototype.replace(searchValue, replaceValue) : string

첫번째 인수로 전달한 문자열 또는 정규표현식을 대상 문자열에서 검색하여 두번째 인수로 전달한 문자열로 대체한다.

`원본 문자열은 변경되지 않고 결과가 반영된 새로운 문자열을 반환`한다.

검색된 문자열이 여럿 존재할 경우 첫번째로 검색된 문자열만 대체된다.

- searchValue: 문자 or 정규표현식
- replaceValue: 문자 or 콜백함수

```tsx
const str = 'Hello world';

// 첫번째로 검색된 문자열만 대체하여 새로운 문자열을 반환한다.
str.replace('world', 'Lee'); // Hello Lee

// 특수한 교체 패턴을 사용할 수 있다. ($& => 검색된 문자열)
str.replace('world', '<strong>$&</strong>'); // Hello <strong>world</strong>

/* 정규표현식
g(Global): 문자열 내의 모든 패턴을 검색한다.
i(Ignore case): 대소문자를 구별하지 않고 검색한다.
*/
str.replace(/hello/gi, 'Lee'); // Lee world
```

```tsx
const camelCase = 'helloWorld';

// 두번째 인수로 치환 함수를 전달할 수 있다.
// 특정 문자를 검색해 모두 대문자로 치환 하는 코드
// 문자를 찾아 인수로 match에 대입해 함수 실행
camelCase.replace('World', (match) => match.toUpperCase()); // "helloWORLD"

// /.[A-Z]/g => 1문자와 대문자의 조합을 문자열 전체에서 검색한다.
camelCase.replace(/.[A-Z]/g, function (match) {
  // match : oW => match[0] : o, match[1] : W
  return match[0] + '_' + match[1].toLowerCase();
}); // hello_world

// /(.)([A-Z])/g => 1문자와 대문자의 조합
// $1 => (.)
// $2 => ([A-Z])
camelCase.replace(/(.)([A-Z])/g, '$1_$2').toLowerCase(); // hello_world
```

#### 정규식

```tsx
.replace(' ','') // 첫번째 공백 제거

.replace(/\-/g,'') // 특정문자 제거1 (-)

.replace(/,/g,'') // 특정문자 제거2(,)

.replace(/^\s+/,'') // 앞의 공백 제거

.replace(/\s+$/,'') // 뒤의 공백 제거

.replace(/^\s+|\s+$/g,'') // 앞뒤 공백 제거

.replace(/\s/g,'') // 문자열 내의 모든 공백 제거

.replace(/\n/g,'') // n개행 제거

.replace(/\r/g,'') // 엔터 제거
```

### String.prototype.split(separator, limit) : string[]

첫번째 인수로 전달한 문자열 또는 정규표현식을 대상 문자열에서 검색하여 문자열을 구분한 후 분리된 각 문자열로 이루어진 배열을 반환한다.

원본 문자열은 변경되지 않는다.

인수가 없는 경우, 대상 문자열 전체를 단일 요소로 하는 배열을 반환한다.

```tsx
const str = 'How are you doing?';

// 공백으로 구분(단어로 구분)하여 배열로 반환한다
console.log(str.split(' ')); // [ 'How', 'are', 'you', 'doing?' ]

// 각 문자를 모두 분리한다
console.log(str.split('')); // [ 'H','o','w',' ','a','r','e',' ','y','o','u',' ','d','o','i','n','g','?' ]

// 정규 표현식
console.log(str.split(/\s/)); // [ 'How', 'are', 'you', 'doing?' ]

// 인수가 없는 경우, 대상 문자열 전체를 단일 요소로 하는 배열을 반환한다.
console.log(str.split()); // [ 'How are you doing?' ]

// 공백으로 구분하여 배열로 반환한다. 단 요소수는 3개까지만 허용한다
console.log(str.split(' ', 3)); // [ 'How', 'are', 'you' ]

// 'o'으로 구분하여 배열로 반환한다.
console.log(str.split('o')); // [ 'H', 'w are y', 'u d', 'ing?' ]
```

### String.prototype.substring(star, end) : string

첫번쨰 인수로 전달한 start 인덱스에 해당하는 문자부터 두번째 인자가 전달된 end 인덱스에 해당하는 문자의 바로 이전 문자까지를 모두 반환한다.

```tsx
const str = 'Hello World'; // str.length == 11

str.substring(1, 4); // ell

// 첫번째 인수 > 두번째 인수 : 순서 맞추기 위해 자동 교환된다.
str.substring(4, 1); // ell

// 두번째 인수가 생략된 경우 : 해당 문자열의 끝까지 반환한다.
str.substring(4); // o World
str.substring(4); // o World

// 인수 < 0 또는 NaN인 경우 : 0으로 취급된다.
str.substring(-2); // Hello World

// 인수 > 문자열의 길이(str.length) : 인수는 문자열의 길이(str.length)으로 취급된다.
str.substring(1, 12); // ello World
str.substring(11); // '' str[10] == 'd'
str.substring(20); // ''
str.substring(0, str.indexOf(' ')); // 'Hello'
str.substring(str.indexOf(' ') + 1, str.length); // 'World'
```

### String.prototype.slice(start, end) : string

substring과 동일하다.
하지만 String.prototype.slice는 음수의 인수를 전달 할 수 있다.

```tsx
const str = 'hello world';

// 인수 < 0 또는 NaN인 경우 : 0으로 취급된다.
str.substring(-5); // 'hello world'
// 뒤에서 5자리를 잘라내어 반환한다.
str.slice(-5); // 'world'

// 2번째부터 마지막 문자까지 잘라내어 반환
tr.substring(2); // llo world
str.slice(2); // llo world

// 0번째부터 5번째 이전 문자까지 잘라내어 반환
str.substring(0, 5); // hello
str.slice(0, 5); // hello
```

### String.prototype.toLowerCase() : string

대상 문자열을 모두 소문자로 변경한다.

### String.prototype.toUpperCase() : string

대상 문자열의 모든 문자를 대문자로 변경한다.

### String.prototype.trim() : string

대상 문자열 양쪽 끝에 있는 공백 문자를 제거한 문자열을 반환한다.

```tsx
const str = '   foo  ';

console.log(str.trim()); // 'foo'

// String.prototype.replace
console.log(str.replace(/\s/g, '')); // 'foo'
console.log(str.replace(/^\s+/g, '')); // 'foo  '
console.log(str.replace(/\s+$/g, '')); // '   foo'

// String.prototype.{trimStart,trimEnd} : Proposal stage 3
console.log(str.trimStart()); // 'foo  '
console.log(str.trimEnd()); // '   foo'
```

### String.prototype.repeat(count) : string

인수로 전달한 숫자만큼 반복해 연결한 새로운 문자열을 반환한다.

count가 0이면 빈 문자열을 반환하고 음수면 RangeError를 발생시킨다.

```tsx
'abc'.repeat(0); // ''
'abc'.repeat(1); // 'abc'
'abc'.repeat(2); // 'abcabc'
'abc'.repeat(2.5); // 'abcabc' (2.5 → 2)
'abc'.repeat(-1); // RangeError: Invalid count value
```

### String​.prototype​.includes(searchString, position) : boolean

인수로 전달한 문자열이 포함되어 있는지를 검사하고 결과를 불리언 값으로 반환한다.

두번째 인수는 옵션으로 검색할 위치를 나타내는 정수이다.

```tsx
const str = 'hello world';

str.includes('hello'); // true
str.includes('hello', 0); // true
str.includes('hello', 2); // false

// String​.prototype​.indexOf 메소드로 대체할 수 있다.
str.indexOf('hello'); // 0
```

### String​.prototype​.padStart(targetLength [, padString])

첫번째 인수로 전체 스트링 길이를 지정하고, 만일 현재 문자열의 길이가 인수보다 짧으면, 그 빈 나머지를 두 번째 인수값으로 채운다.

```tsx
'abc'.padStart(10); // "       abc"
'abc'.padStart(10, 'foo'); // "foofoofabc"
'abc'.padStart(6, '123465'); // "123abc"
'abc'.padStart(8, '0'); // "00000abc"
'abc'.padStart(1); // "abc"
```
