---
title: "배열과 객체 다루기"

categories:
  - "js"
tags:
  - [js]

toc: true
toc_sticky: true

date: 2022-03-05
last_modified_at: 2022-03-05
---

<div style="margin-bottom:41px"></div>

배열과 객체를 이용하여 데이터를 어떻게 처리해야 할지 몰라서 커뮤니티에 질문을 하였는데, 커뮤니티에서 사이트 추천을 해주셔서 정리 해보기로 하였다.

### 1. 숫자/문자열 배열에서 중복 제거하기

```js
let values = [3, 1, 3, 5, 2, 4, 4, 4];
let uniqueValues = [...new Set(values)]; // Set는 배열에서 중복된 값을 허용하지 않는 특징을 가짐, ES6에서 새롭게 도입
// [3,1,5,2,4]
```

### 2. 간단한 검색(case-sensitive)

filter함수는 인자로 제공되는 함수에 의해 test를 통과한 모든 요소를 새로운 array로 만듦

```js
let users = [
  { id: 11, name: "John", age: 23, group: "editor" },
  { id: 47, name: "Tom", age: 28, group: "admin" },
  { id: 84, name: "Bread", age: 34, group: "editor" },
  { id: 33, name: "Holand", age: 27, group: "admin" },
];

let res = users.filter((it) => it.name.includes("Bre"));

// filter는 true인 요소를 모아 새로운 배열로 리턴
// includes는 배열이 특정 요소를 포함하면 true, 아니면 false 반환

//  { id: 84, name: "Bread", age: 34, group: "editor" },
```

### 3. 간단한 검색(case-insensitive)

```js
let users = [
  { id: 11, name: "John", age: 23, group: "editor" },
  { id: 47, name: "Tom", age: 28, group: "admin" },
  { id: 84, name: "Bread", age: 34, group: "editor" },
  { id: 33, name: "Holand", age: 28, group: "admin" },
];

let res = users.filter((it) => new RegExp("Bre", "i").test(it.name));

// 정규식 표현으로 Bre을 나타내고 대소문자를 무시하고 찾기
//  { id: 84, name: "Bread", age: 34, group: "editor" },
```

### 4. 특정 유저가 admin 권한을 갖고 있는지 확인

```js
let users = [
  { id: 11, name: "John", age: 23, group: "editor" },
  { id: 47, name: "Tom", age: 28, group: "admin" },
  { id: 84, name: "Bread", age: 34, group: "editor" },
  { id: 33, name: "Holand", age: 28, group: "admin" },
];

let hasAdmin = users.some((user) => user.group === "admin");

// users.group에 admin이 있기 때문에 true를 반환한다.
```

### 5. array of arrays 펼치기

```js
let nested = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
];
let flat = nested.reduce((acc, it) => [...acc, ...it], []);
// 1 cycle : acc => [], it => [ 1, 2, 3 ]
// 2 cycle : acc => [1, 2, 3], it => [ 4, 5, 6 ]
// 3 cycle : acc => [1, 2, 3, 4, 5, 6], it => [ 7, 8, 9 ]

// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

reduce안에서 spread operator는 좋은 성능을 보이지 못해 아래와 같이 표현 가능.

```js
let flat = [].concat.apply([], nested);

// concat의 arguments로 nested의 단일 요소로 새로운 배열로 추가

let flat = [].concat([], ...nested);
// spread operator형식으로도 가능
```

### 6. 특정 키의 빈도를 포함하는 객체를 만들기

```js
let users = [
  { id: 11, name: "John", age: 23, group: "editor" },
  { id: 47, name: "Tom", age: 28, group: "admin" },
  { id: 84, name: "Bread", age: 34, group: "editor" },
  { id: 33, name: "Holand", age: 28, group: "admin" },
];
let groupByAge = users.reduce(
  (acc, it) => ({ ...acc, [it.age]: (acc[it.age] || 0) + 1 }),
  // (acc[it.age]이 있으면 (acc[it.age]의 값에 1을 더하고 없으면 1로 초기화
  {}
);

// 1 cycle : acc => {}, it => {'23': 1}  acc[it.age]값에 값이 없으니 {'23' : 1}이 됨
// 2 cycle : acc => {'23': 1}, it => {'28' : 1}  acc[it.age]값에 값이 없으니 {'28' : 1}이 됨
// 3 cycle : acc => {'23' : 1, '28' : 1}, it => {'34' : 1} acc[it.age]값에 값이 없으니 {'34' : 1}이 됨
// 4 cycle : acc => {'23' : 1, '28' : 1, '34' : 1}, it => {'28' : 2} acc[it.age]에 {'28' : 1}가 있으니 원래의 값 1에 1을 더함

// { '23': 1, '28': 2, '34': 1 }
```

### 7. array of object 인덱싱 (lookup table)

id로 유저를 찾기 위해 전체 array를 처리하는 것 대신에 user's id가 key로 작용하는 객체를 만들 수 있다.

```js
let users = [
  { id: 11, name: "John", age: 23, group: "editor" },
  { id: 47, name: "Tom", age: 28, group: "admin" },
  { id: 84, name: "Bread", age: 34, group: "editor" },
  { id: 33, name: "Holand", age: 28, group: "admin" },
];
let uTable = users.reduce((acc, it) => ({ ...acc, [it.id]: it }), {});
// it.id(users의 id의 값)가 키가 되고, it(즉 users의 요소)가 값이 되는 객체를 uTable 변수에 저장

uTable result :
{
  '11': { id: 11, name: 'John', age: 23, group: 'editor' },
  '33': { id: 33, name: 'Holand', age: 28, group: 'admin' },
  '47': { id: 47, name: 'Tom', age: 28, group: 'admin' },
  '84': { id: 84, name: 'Bread', age: 34, group: 'editor' }
}

console.log(uTable[84])
 { id: 84, name: 'Bread', age: 34, group: 'editor' }


console.log(uTable[84].name) // id로 데이터를 접근할때 유용하다
Bread
```

### 8. 배열 안의 각각의 item에서 특정 키로 유일한 값을 뽑아내기

```js
let users = [
  { id: 11, name: "John", age: 23, group: "editor" },
  { id: 47, name: "Tom", age: 28, group: "admin" },
  { id: 84, name: "Bread", age: 34, group: "editor" },
  { id: 33, name: "Holand", age: 28, group: "admin" },
];

let listOfUserGroups = [...new Set(users.map((it) => it.group))];
// Set : 중복되지 않는 유일한 값들의 집합

users.map((it)=>it.group)  // [ 'editor', 'admin', 'editor', 'admin' ]
new Set(users.map((it)=>it.group)) // Set(2) { 'editor', 'admin' }
...new Set(users.map((it)=>it.group))  // editor admin
[...new Set(users.map((it) => it.group))]  // [ 'editor', 'admin' ]

listOfUserGroups result :
 ["editor", "admin"];
```

## 참조

- [map, reduce, filter를 유용하게 활용하는 15가지 방법](https://dongmin-jang.medium.com/javascript-15%EA%B0%80%EC%A7%80-%EC%9C%A0%EC%9A%A9%ED%95%9C-map-reduce-filter-bfbc74f0debd)
