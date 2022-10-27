# 숫자형

`.toString(base)`

숫자 대상으로 호출은 `..toString()`

`Math.trunc()` 소수부 무시

`.toFixed(n)` 반올림 후 문자열 반환

`NaN`은 서로 같지 않음. `isNaN()`을 사용

`isFinite()` 문자열이 일반 숫자인지 검증

`Object.is()`를 이용한 비교

## 변환

`parseInt(str, radix)`, `parseFloat()`

`+`, `Number()`

## 기타 수학 함수

`Math.random()` 0과 1 사이 난수 반환

`Math.max(a, b, c, ...)`, `Math.min(a, b, c, ...)`

`Math.pow(n, power)`

---

# 문자열

백틱으로 여러 줄 문자열 작성 가능

`.length` 문자열의 길이 (메서드가 아니라 프로퍼티)

글자에 접근은 대괄호`[pos]` 이용. 없으면 `undefined`

`.charAt(pos)`은 없으면 빈 문자열 반환

`for..of`로 반복 작업

`.toUpperCase()`, `toLowerCase()`

## 부분 문자열

`.indexOf(substr, pos)` 없으면 `-1` 반환

`.lastIndexOf(substr, pose)` 끝에서부터 탐색

`includes()`, `startsWith()`, `endsWith()` 있으면 `true`, 없으면 `false`

### 부분 문자열 추출

`.slice(start [, end])` start부터 end까지 반환 (end 미포함) 음수 가능

`.substring(start [, end])` start가 end보다 커도 괜찮음. 음수 불가능 (음수는 0으로 처리)

`.substr(start [, length])` start부터 시작해 length개의 글자 반환. 음수면 뒤에서부터 셈

`slice()`를 주로 많이 사용

---

# 배열

```javascript
let arr = new Array();
let arr = [];
```

인덱스 지정해서 새로운 요소 추가 가능

```javascript
let arr = [1, 2, 3];
arr[3] = 4; // [1, 2, 3, 4]
```

`.pop()`, `.shift()`

`.push()`, `.unshift()`

## 반복문

`for (let i = 0; i < arr.length; i++) {}`

`for..of` -> `for (let a of arr) {}`

`for..in`은 배열에는 쓰지 말고 객체형(배열이 객체형이긴 하지만)에만 사용

---

```javascript
arr.length = 0; // 배열 비우기
```

`new Array()`

```javascript
let arr = new Array("1", "2", "3");
```

`new Array()`에 숫자형 인수 하나 넣으면 요소가 없지만 길이는 인수인 배열 생성

`.toString()` 요소를 쉼표로 구분한 문자열 반환

## 요소 추가, 제거

`.push(...items)`, `.pop()`, `.shift()`, `.unshift(...items)`

`delete` 사용하면 요소 없애도 길이는 변하지 않음

`.splice(index[, deleteCount, elem1, ..., elemN])` 음수 인덱스도 가능

`.slice([start], [end])` 간단하게 배열 복사본 생성 가능

`.concat(arg1, arg2, ...)` 기존 배열에 추가

```javascript
let arr = [1, 2];
let arrayLike = {
  0: "something",
  length: 1,
};
arr.concat(arrayLike); // 1,2,[object Object]
```

`[Symbol.isConcatSpreadable]: true,`가 있으면 배열처럼 취급

```javascript
let arr = [1, 2];
let arrayLike = {
  0: "something",
  1: "else",
  [Symbol.isConcatSpreadable]: true,
  length: 2,
};
arr.concat(arrayLike); // 1,2,something,else
```

## 반복

`.forEach(function(item, index, array) {})`

## 탐색

`.indexOf(item, from)` 있으면 인덱스, 없으면 `-1`

`.lastIndexOf(item, from)`

`.includes(item, from)` 발견하면 `ture`

`.find(function(item, index, arry) {})` 초건에 해당하는 요소 발견시 해당 요소 반환. 없으면 `undefined`

`.findIndex()`는 `.find()`와 같은 일을 하나 조건에 맞는 요소 반환 대신 해당 요소의 인덱스 반환. 맞는 요소 없으면 `-1`

`.filter(function(item, index, array) {})` 조건 충족 요소가 여러개인 경우 사용. 조건에 맞는 요소 전체를 담은 배열 반환

## 배열 변형 메서드

`.map(function(item, index, array) {})` 배열 요소 전체를 대상으로 함수 호출하고 결과를 배열로 반환

`.sort(fn)` 배열의 요소 정렬 (문자열로 취급해서 정렬!!) 정수 배열을 정렬하고 싶다면 정수 크기를 비교하는 함수를 넘겨줌

정수 비교하는 경우 보통 아래처럼 사용

```javascript
let arr = [1, 2, 15];
arr.sort((a, b) => a - b); // [1, 2, 15]
```

`.reverse()`

`.split(delim)` 구분자(delimiter)를 기준으로 문자열 쪼갬

`.join(glue)` 접착제를 기준으로 요소 붙여 하나의 문자열 생성

`.reduce()`, `.reduceRight()` 배열을 기반으로 값 하나 도출

```javascript
let value = arr.reduce(
  function (accumulator, item, index, array) {
    // ...
  },
  [initial]
);
```

`accumulator`: 이전 함수의 호출 결과 (다음 함수를 호출할 때 첫 번째 인수로 사용)

`item`: 현재 배열 요소

`index`: 요소의 위치

`array`: 배열

`initial`: 함수 최초 호출시 사용되는 초깃값

```javascript
let arr = [1, 2, 3, 4, 5];
let result = arr.reduce((sum, current) => sum + current, 0); // 15
```

## 배열 여부

`Array.isArray()`

## 유사 배열을 배열로 변환

`Array.from()`

---

# 맵과 셋

## 셋

중복을 허용하지 않음

`new Set(iterable)` 셋 생성 (대개 배열 전달)

`.add(value)` 값 추가 후 셋 자신 반환

`.delete(value)` 값 제거 성공 `true`, 실패 `false`

`.has(value)` 셋 내에 값 존재하면 `true`, 아니면 `false`

`.clear()` 셋 비움

`.size` 값 개수

```javascript
let set = new Set();

let john = { name: "John" };
let pete = { name: "Pete" };
let mary = { name: "Mary" };

// 어떤 고객(john, mary)은 여러 번 방문할 수 있습니다.
set.add(john);
set.add(pete);
set.add(mary);
set.add(john);
set.add(mary);

// 셋에는 유일무이한 값만 저장됩니다.
alert(set.size); // 3

for (let user of set) {
  alert(user.name); // // John, Pete, Mary 순으로 출력됩니다.
}
```

`for..of`, `.forEach()`를 사용해 반복 작업

```javascript
let set = new Set(["oranges", "apples", "bananas"]);

for (let value of set) alert(value);

// forEach를 사용해도 동일하게 동작합니다.
set.forEach((value, valueAgain, set) => {
  alert(value);
});
```

`.keys()` 셋 내의 모든 값을 포함하는 이터러블 객체 반환

`.values()`는 `.keys()`와 동일한 작업을 함. 맵과의 호환성을 위함

`.entries()` 셋 내의 각 값을 이용해 만든 `[value, value]` 배열을 포함하는 이터러블 객체 반환. 맵과의 호환성을 위함

---

# Object.keys, values, entries

일반 객체 메서드

`Object.keys(obj)` 객체의 키만 담은 배열 반환

`Object.values(obj)` 객체의 값만 담은 배열 반환

`Object.entries(obj)` `[키, 값]` 쌍을 담은 배열 반환

## 객체 변환하기

객체에 배열 전용 메서드를 사용할 수 없지만, 변환을 통해 가능

```javascript
let prices = {
  banana: 1,
  orange: 2,
  meat: 4,
};

let doublePrices = Object.fromEntries(
  // 객체를 배열로 변환해서 배열 전용 메서드인 map을 적용하고 fromEntries를 사용해 배열을 다시 객체로 되돌립니다.
  Object.entries(prices).map(([key, value]) => [key, value * 2])
);

alert(doublePrices.meat); // 8
```

---

# 구조 분해 할당

## 배열 분해

```javascript
let [firstName, surname] = arr;
let [firstName2, surname2] = "Bora Lee".split(" ");
// 두 번째 요소는 필요하지 않음
let [firstName, , title] = [
  "Julius",
  "Caesar",
  "Consul",
  "of the Roman Republic",
];
```

할당 연산자 우측엔 모든 이터러블 가능

할당 연산자 좌측엔 할당할 수 있는 것이라면 뭐든 가능

```javascript
let user = {
  name: "John",
  age: 30,
};

// 객체의 키와 값 순회하기
for (let [key, value] of Object.entries(user)) {
  alert(`${key}:${value}`); // name:John, age:30이 차례대로 출력
}
```

변수 교환 트릭

```javascript
let guest = "Jane";
let admin = "Pete";

// 변수 guest엔 Pete, 변수 admin엔 Jane이 저장되도록 값을 교환함
[guest, admin] = [admin, guest];

alert(`${guest} ${admin}`); // Pete Jane(값 교환이 성공적으로 이뤄졌습니다!)
```

'...'로 나머지 요소 가져오기

```javascript
let [name1, name2, ...rest] = [
  "Julius",
  "Caesar",
  "Consul",
  "of the Roman Republic",
];
```

기본값

```javascript
let [firstName, surname] = []; // undefined, undefined
```

```javascript
let [name = "Guest", surname = "Anonymous"] = ["Julius"]; // Julius, Anonymous
```

복잡한 표현식, 함수 호출도 기본값이 될 수 있음

## 객체 분해

`let {var1, var2} = {var1:..., var2:...}`

객체 프로퍼티, 목표 변수

`let {width: w, height: h, title} = options;`

할당 연산자까지 사용

`let {width: w = 100, height: h = 200, title} = options;`

나머지 패턴 '...'

`let {title, ...rest} = options;`

## 중첩 구조 분해

---

# JSON과 메서드

`JSON.stringify()` 객체를 JSON으로

`JSON.parse()` JSON을 객체로
