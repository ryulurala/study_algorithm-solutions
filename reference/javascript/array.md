---
title: "JavaScript Array"
excerpt: "Array of JavaScript"
category: JavaScript-Reference
tags: [JavaScript, array]
toc: true
---

## Array of JavaScript

### 반복문(forEach, some)

- `.some((value, index, arr) => {})`
  > Array Method 로서 배열의 요소 반복 작업 가능  
  > 중간에 `Only. return true;`으로 `break;` 안해도 무방(**권장!!**)  
  > value: 원소 값  
  > index: 인덱스  
  > arr: array 배열 그 자체
- `.forEach((value, index, arr) => {})`
  > Array Method 로서 배열의 요소 반복 작업 가능  
  > 중간에 `break;` **불가능**, 모든 요소 작업  
  > value: 원소 값  
  > index: 인덱스  
  > arr: array 배열 그 자체

```js
let arr = [1, 2, 3, 4, 5];

arr.some((value, index, array) => {
  console.log(value); // 현재 Array index의 원소 값 출력
  console.log(index); // index 출력
  console.log(array); // [1, 2, 3, 4, 5] 출력
  // 중간에 break; 가능
  if (value === 3) return true; // false하면 break 안됨
});

arr.forEach((value, index, array) => {
  console.log(value); // 현재 Array index의 원소 값 출력
  console.log(index); // index 출력
  console.log(array); // [1, 2, 3, 4, 5] 출력
});
```

### 초기화된 Array 선언

- `Array.from({length: N}, (value, index) => index)`
  > 초기화된 Array 선언 가능  
  > value: 원소 값이지만 어차피 undefined  
  > index: 인덱스

```js
let array1 = Array.from({ length: 5 }, (value, index) => {
  return index; // [0, 1, 2, 3, 4] 로 초기화된 Array 생성
});

let array2 = Array.from([1, 2, 3], (value) => value * 2); // [2, 4, 6] Array 생성
```

### 요소 검색, 존재 여부

- `array.indexOf(variable)`
  > array 앞에서부터 variable 값을 찾아서 Index 리턴, 없으면 -1 리턴
- `array.lastIndexOf(variable)`
  > array 뒤에서부터 variable 값을 찾아서 Index 리턴, 없으면 -1 리턴
- `array.includes(variable)`
  > array 안에 variable 값이 있으면 true, 없으면 false 리턴
- `array.includes(num, fromIndex)`
  > array 안에 fromIndex 부터 variable 값이 있으면 true, 없으면 false 리턴

+++++

- `array.find(function(value, index, arr){return 조건})`
  > 기본적으로 undefined 리턴  
  > value: 원소 값  
  > index: 인덱스  
  > arr: array 배열 그 자체  
  > 찾으면 value 값 리턴

```js
let array = [1, 4, 3, 4, 5];

// 속도 includes() > indexOf()
array.includes(1); // true
array.includes(1, 2); // false, index 2 부터 1을 찾는다

array.indexOf(4); // 1 리턴, 찾으면 바로 리턴
array.indexOf(6); // -1 리턴
array.lastIndexOf(4); // 3 리턴, 찾으면 바로 리턴
array.lastIndexOf(6); // -1 리턴

// +++++

array.find((value, index, arr) => {
  return value > 2; // 2보다 큰 원소를 찾으면 해당 value 리턴, 못찾으면 undefined 리턴
});

array.find((item, index));
```

### 교체, 삽입, 삭제

- `array.slice(startIndex, endIndex)`
  > startIndex 부터 endIndex 전까지 복제본 리턴  
  > 원본 변경 X  
  > endIndex를 지정하지 않을 경우 끝까지 복제  
  > `array.slice()` 로 깊은 복사 가능
- `array.splice(startIndex, deleteCount, value1, value2, ...)`
  > startIndex부터 deleteCount개수만큼 삭제하고 value1, value2, ...로 교체  
  > 원본 변경  
  > deleteCount를 0으로 할 경우 삽입 가능  
  > value를 지정하지 않을 경우 삭제 가능

```js
let array = [1, 2, 3, 4, 5, 6, 7];

array.slice(); // 깊은 복사
array.slice(2); // [3, 4, 5, 6, 7]
array.slice(2, 5); // [3, 4, 5]
console.log(array); // [1, 2, 3, 4, 5, 6, 7]

console.log(array.splice(1, 4, 11, 12)); // [2, 3, 4, 5]
console.log(array); // [1, 11, 12, 6, 7]
array.splice(2, 0, 10, 11); // Index: 2에 10, 11 삽입
```

### `map()`, `filter()`, `find()`, `reduce()`

- `map(function(value, index, array){})`
  > Array의 요소를 일괄적으로 변경(Mapping)  
  > 부모 스코프 건드리지 않고 Array 리턴
- `filter(function(value, index, array){})`
  > Array의 요소를 걸러냄(Filtering)  
  > 부모 스코프 건드리지 않고 Array 리턴
- `find(function(value, index, array){})`
  > Array의 요소를 찾아냄(Finding)  
  > 요소 하나만을 리턴
- `reduce(function(prev, value){}, initialValue)`
  > 이전 리턴된 prev 값과 현재 값 value 를 이용하여 활용 가능(만능)  
  > 처음 시작 prev 값의 initialValue 지정. ex) `prev = 0;` or `prev = [];`  
  > 부모 스코프 건드리지 않고 Array 리턴

```js
let arr = [1, 2, 3, 4, 5];

let mapResult = arr.map((value, index, array) => {
  return value * 2;
});
console.log(mapResult); // [2, 4, 6, 8, 10]

let filterResult = arr.filter((value, index, array) => {
  return value % 2 == 0;
});
console.log(filterResult); // [2, 4]

let findResult = arr.find((value, index, array) => {
  return value % 2 == 0;
});
console.log(findResult); // 2

let reduceResult1 = arr.reduce((prev, value) => {
  return prev + value;
}, 0);
console.log(reduceResult1); // 15

let reduceResult2 = arr.reduce((prev, value) => {
  prev.push(value * 2);
  return prev;
}, []); // [2, 4, 6, 8, 10]
```
