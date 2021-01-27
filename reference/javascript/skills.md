---
title: "JavaScript Skills"
excerpt: "Skills by JavaScript"
category: JavaScript-Reference
tags: [JavaScript, compare, sort, math]
toc: true
---

## Skills by JavaScript

### 순열(Permutation), 조합(Combination)

- 기본 규칙

  > 배열에서 N개를 선택하는 경우,
  >
  > 1. 하나의 수를 선택.
  > 2. 남은 배열에서 나머지 N-1개를 선택.

- 순열(Permutation)
  > 만약, `selectNum`이 1개일 경우, 배열의 각각 요소가 순열이므로 하나의 작은 배열로 변환  
  > 입력 받은 `arr`를 forEach로 순회하며 먼저 뽑을 1개(`fixed`)를 선택.  
  > `fixed`를 제외한 나머지 배열(`restArr`)를 생성(filter로 해당 인덱스 제외)  
  > `restArr`로 `selectNum-1`의 재귀로 돌린 결과가 `permutationArr`에 저장  
  > `result`에 전개 연산자 `...`로 push(깊은 복사)

```js
const permutation = (arr, selectNum) => {
  const result = [];
  if (selectNum === 1) return arr.map((v) => [v]);
  else {
    arr.forEach((value, idx) => {
      const fixed = value; // 1개 선택
      const restArr = arr.filter((v, i) => i !== idx); // 나머지 배열
      const permutationArr = permutation(restArr, selectNum - 1); // 나머지 배열의 결과
      const mergeArr = permutationArr.map((v) => [fixed, ...v]); // 합치기
      result.push(...mergeArr); // 깊은 복사로 push
    });
    return result;
  }
};

permutation([1, 2, 3], 1); // [ [1], [2], [3] ]
permutation([1, 2, 3], 2); // [ [1, 2], [1, 3], [2, 1], [2, 3], [3, 1], [3, 2] ]
permuation([1, 2, 3], 3); // [ [1, 2, 3], [1, 3, 2], [2, 1, 3], [2, 3, 1], [3, 1, 2], [3, 2, 1] ]
```

- 조합(Combination)
  > 순열과 과정은 동일하다.  
  > 한 번 선택했던 수는 다시 선택할 필요가 없으므로 `slice(index+1)`을 해줌.

```js
const combination = (arr, selectNum) => {
  const result = [];
  if (selectNum === 1) return arr.map((v) => [v]);
  else {
    arr.forEach((value, idx) => {
      const fixed = value;
      const restArr = arr.slice(idx + 1); // 다시 선택할 필요 X
      const permutationArr = combination(restArr, selectNum - 1);
      const mergeArr = permutationArr.map((v) => [fixed, ...v]);
      result.push(...mergeArr);
    });
    return result;
  }
};

combination([1, 2, 3], 1); // [ [1], [2], [3] ]
combination([1, 2, 3], 2); // [ [1, 2], [1, 3], [2, 3] ]
combination([1, 2, 3], 3); // [[1, 2, 3]]
```

- 중복 순열
  > 순열과 과정은 동일하다.  
  > 선택을 하더라도 중복해서 선택할 수 있으므로 세 번째 인자(`array`)를 나머지 배열로 사용

```js
const overPermutation = (arr, selectNum) => {
  const result = [];
  if (selectNum === 1) return arr.map((v) => [v]);
  else {
    arr.forEach((value, idx, array) => {
      const fixed = value;
      const restArr = array; // 기존 배열로 계속 순열
      const permutationArr = overPermutation(restArr, selectNum - 1);
      const mergeArr = permutationArr.map((v) => [fixed, ...v]);
      result.push(...mergeArr);
    });
    return result;
  }
};

overPermutation([1, 2], 1); // [ [1], [2] ]
overPermutation([1, 2], 2); // [ [1, 1], [1, 2], [2, 1], [2, 2] ]
```

### 정렬(sort) only. Array

- about `JavaScript-Sort`

  > JavaScript의 sort()의 기본은 Quick-Sort이고 Stable-Sort가 아니다.  
  > `-1`을 리턴하면 바뀌는 원리(`C++`과 동일)

- `sort(function(){});`

  > function() 정렬 함수  
  > sort(): 기본 오름차순 정렬

- 오름차순(ascending) --- `function(a, b)`
  > b값이 더 크면 음수(-1)가 리턴되어 바뀌는 것을 이용  
  > `return a-b;`  
  > `return (a<b) ? -1 : (a===b) ? 0 : 1;`
- 내림차순(descending) --- `function(a, b)`
  > a값이 더 크면 음수(-1)가 리턴되어 바뀌는 것을 이용  
  > `return b-a;`  
  > `return (b<a) ? -1 : (a===b) ? 0 : 1;`

```js
let numbers = [1, 5, 2, 4, 3];
let fruits = [
  { name: "apple", cost: 100 },
  { name: "banana", cost: 400 },
  { name: "strawberry", cost: 200 },
  { name: "grape", cost: 300 },
];

numbers.sort((a, b) => {
  return a - b; // 오름차순 정렬 --- 1, 2, 3, 4, 5
});
numbers.sort((a, b) => {
  return b - a; // 내림차순 정렬 --- 5, 4, 3, 2, 1
});

fruits.sort((item1, item2) => {
  return item1.cost - item2.cost; // 비용으로 오름차순 정렬
});

fruits.sort((item1, item2) => {
  return item1.cost - item2.cost; // 비용으로 내림차순 정렬
});

fruits.sort((a, b) => {
  // 오름차순(사전 정렬)
  if (a < b) return -1;
  else if (a > b) return 1;
  else return 0;
});

fruits.sort((a, b) => {
  // 내림차순
  if (a > b) return -1;
  else if (a < b) return 1;
  else return 0;
});
```

### 문자열 or 배열 이어붙이기

- `variable.concat(var1, var2, ...)`
  > `array.concat()` or `str.concat()` 모두 가능  
  > 원본 변경 X  
  > 이어붙인 복제본 리턴

```js
[1, 2, 3].concat(4, 5, 6); // [1, 2, 3, 4, 5, 6]
"hi".concat(" hello"); // "hi hello"
```

### 문자열을 숫자로 바꾸기

- `parseInt(str)`
  > str 문자열을 정수로 바꿔서 리턴
- `parseFloat(str)`
  > str 문자열을 실수로 바꿔서 리턴
- `+str` or `str*1` or `str/1`
  > 문자열과 숫자와 사칙 연산을 하면 숫자로 바뀜 **중요!!**

```js
Number.parseInt("-123.4"); // -123
Number.parseFloat("-123.4"); // -123.4
"-123.4" * 1; // -123.4
+"-123.4"; // -123.4
```

### 비교연산자('==' vs '===')

- `==` / `!=`
  > 비교 연산자: 형 변환 후 값을 비교
- `===` / `!==`
  > 일치 연산자: 형 변환 X 비교, 엄격(Strict) **권장!!**

```js
let zero1 = 0;
let zero2 = "0";

if (zero1 == zero2); // true
if (zero1 === zero2); // false
```

### 출력(console.log)

- `console.log(variable1, variable2, ...)`
  > 변수 출력: variable1 variable2 출력됨.(',' 출력 X)
- `console.log(array)`
  > 배열 출력: [value1, value2, value3, ...] 출력됨.
- `console.dir(object)` or `console.log(object)`
  > 객체 출력: {key1: value2, key2: value2, ...} 출력됨.  
  > dir(): 속성까지 모두 출력, DOM 객체 출력할 때 권장(브라우저 출력)  
  > 대부분 log 써도 무방

```js
let variable1 = 4;
let variable2 = 5;
let array = [1, 2, 3, 4, 5];
let obj = { name: "ryulurala", age: "26" };

console.log(variable1, variable2); // 4 5 출력
console.log(array); // [1, 2, 3, 4, 5] 출력
console.log(obj); // {name: "ryulurala", age: "26"} 출력
console.dir(obj); // {name: "ryulurala", age: "26"} 출력(브라우저 출력은 다름)
```

### 반복문(for-in, for-of)

- `for(let value of iterables){}`
  > 순서가 없는 (iterable) Array를 순회할 때 권장
- `for(let key in enumerables){}`
  > 순서가 있는 (enumerable) Json 객체를 순회할 때 권장

```js
let array = [1, 2, 3, 4, 5];
let fruits = [
  { name: "apple", cost: 100 },
  { name: "banana", cost: 400 },
  { name: "strawberry", cost: 200 },
  { name: "grape", cost: 300 },
];

for (let fruit of fruits) {
  console.log(fruit); // fruits[0], fruits[1], ..., fruits[3]
  for (let key in fruit) {
    console.log(key, value); // apple 100, banana 400, ..., grape 300
  }
}
```

### Max, Min 값 도출(in Array)

- `Math.max(num1, num2, ...)`
  > num1, num2, ... 중에 최댓값 값 도출
- `Math.min(num1, num2, ...)`
  > num1, num2, ... 중에 최솟값 값 도출
- `Math.max.apply(null, array)` or `Math.max(...array)`
  > array에서 최댓값 도출
- `Math.min.apply(null, array)` or `Math.min(...array)`
  > array에서 최솟값 도출

```js
let array = [1, 5, 4, 3, 2];

let max = Math.max(20, 50); // max = 50
let min = Math.min(20, 50); // min = 20

let maxNum = Math.max.apply(null, array); // maxNum = 5
let minNum = Math.min.apply(null, array); // minNum = 1
```

### 소수점 변환

- 정수 변환

  - `Math.ceil(number)`
    > 소수점 올림, 정수 리턴
  - `Math.floor(number)`
    > 소수점 내림, 정수 리턴
  - `Math.round(number)`
    > 소수점 반올림, 정수 리턴

- 소수 변환
  - `.toFixed(number)`
    > 소수점 num+1 자리에서 반올림 후 num 자리까지 리턴

```js
let num = 10.567;

Math.ceil(num); // 11
Math.floor(num); // 10
Math.round(num); //11

num.toFixed(2); // 10.57
```

### 제곱, 루트, 절댓값

- `Math.pow(base, exponent)`
  > base의 exponent 거듭 제곱 리턴
- `Math.sqrt(number)`
  > number의 제곱근 리턴
- `Math.abs(number)`
  > number의 절댓값 리턴

```js
Math.pow(3, 2); // 3^2 = 9
Math.sqrt(4); // root 4 = 2
Math.abs(-9); // 9
```
