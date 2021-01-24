---
title: "JavaScript Structure"
excerpt: "Structure by JavaScript"
category: JavaScript-Reference
tags: [JavaScript, stack, queue, set, map]
toc: true
toc_sticky: true
---

## Structure of JavaScript

### Stack

- `Array` 이용
  > Stack 처럼 사용 가능
- `array.push(element)`
  > Stack top에 원소 push
- `array.pop()`
  > Stack top에 원소 pop
- `array[array.length-1]`
  > Stack의 top

```js
let stack = [1, 2, 3, 4, 5];

stack.push(6); // [1, 2, 3, 4, 5, 6]
stack.pop(); // [1, 2, 3, 4, 5]
stack[stack.length - 1]; // 5
```

### Queue

- `Array` 이용
  > Queue 처럼 사용 가능
- `array.push(element)`
  > Queue back에 원소 push
- `array.shift()`
  > Queue front에 원소 pop
- `array[0]`
  > Queue의 front
- `array[array.length-1]`
  > Queue의 back

+++++

- `unShift(element)`
  > Array 앞에 원소 추가

```js
let queue = [1, 2, 3, 4, 5];

queue.push(6); // [1, 2, 3, 4, 5, 6]
queue.shift(); // [2, 3, 4, 5, 6]
stack[0]; // 2
stack[queue.length - 1]; // 6

// +++++

queue.unShift(4); // [4, 2, 3, 4, 5, 6]
```

### Map

- about `Map`

  > `(key, value)` pair로 이루어진 collection  
  > key들은 중복 불가: 하나의 key에는 하나의 value 즉, 갱신됨  
  > `get()`, `set()` 으로 조회 및 삽입  
  > `forEach((value, index) => {})`로 접근 가능  
  > `some(function(){})`은 불가

- `new Map()`
  > Map 생성
- `map.set(key, value)`
  > (key, value) pair로 삽입  
  > 중복된 key에 대해 value는 갱신
- `map.get(key)`
  > key 값에 대한 value 값 리턴
- `map.has(key)`
  > key에 해당하는 value 값 있으면 true, 없으면 false
- `map.size`
  > map의 size 리턴
- `map.delete(key)`
  > 해당 key에 해당하는 (key, value) pair 삭제  
  > 삭제 결과 리턴, 삭제 못하면 false
- `map.clear()`
  > map의 모든 (key, value) pair 삭제

```js
let map = new Map();
map.set(1, 2);
map.set(2, 4);
map.set(1, 3);

map.get(1); // 3
map.get(2); // 4
map.size; // 2
map.delete(1); // true
map.delete(4); // false
map.has(1); // false
map.has(2); // true
map.clear();
```

### Set

- about `Set`

  > `value`로 이루어진 집합(collection)  
  > value들은 중복 불가: 중복된 값을 추가하면 아무 일도 발생하지 않음  
  > `add()` 로 삽입  
  > `forEach((value, index) => {})`로 접근 가능  
  > `some(function(){})`은 불가

- `new Set()`
  > Map 생성
- `set.add(value)`
  > value 삽입  
  > 중복된 value 대해 아무 일도 발생 X
- `set.has(value)`
  > value 값이 있으면 true, 없으면 false
- `set.size`
  > set의 size 리턴
- `set.delete(value)`
  > 해당 value 삭제  
  > 삭제 결과 리턴, 삭제 못하면 false
- `set.clear()`
  > set의 모든 value 삭제

```js
let set = new Set();
set.add(1);
set.add(2);
set.add(1);

set.size; // 2
set.delete(1); // true
set.delete(4); // false
set.has(1); // false
set.has(2); // true
set.clear();
```

---
