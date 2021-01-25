---
title: "JavaScript String"
excerpt: "String of JavaScript"
category: JavaScript-Reference
tags: [JavaScript, string]
toc: true
---

## String of JavaScript

### 문자의 ASCII code 값

- `charCodeAt()`
  > 첫 문자 하나의 ASCII Code 값을 리턴한다.

```js
"ABC".charCodeAt(); // 65, 'A'===65
"abc".charCodeAt(); // 97, 'a'===97
```

### 문자열 뒤집기(by Array Method)

- `str.split("").reverse().join("")`
  > a) `split("")` - Array가 됨  
  > b) `reverse()` - Array를 뒤집음  
  > c) `join("")` - 다시 문자열화

```js
let str = "hihi";
str = str.split(""); // ["h", "i", "h", "i"]
str = str.reverse(); // ["i", "h", "i", "h"]
str = str.join(""); // "ihih"

// 위와 같은 메소드(Promise 이용)
str = "hihi".split("").reverse().join("");
```

### 부분 문자열

- `str.substring(startIndex, endIndex)`
  > str 문자열의 startIndex부터 endIndex 전까지 부분 문자열을 리턴  
  > 원본 변경 X

```js
"string".substring(1, 3); // "tr" 리턴
```

### 대문자, 소문자 변환

- `str.toUpperCase()`
  > str을 대문자들로 변환
- `str.toLowerCase()`
  > str을 소문자들로 변환

```js
"StRing".toUpperCase(); // "STRING" 리턴
"StRing".toLowerCase(); // "string" 리턴
```

### 공백 제거

- `str.trim()`
  > 앞뒤 공백 제거

```js
"   string    ".trim(); // "string" 리턴
```

### 구분자로 나눔 or 합침

- `str.split(separator)`
  > separator(구분자)로 나눔
- `array.join(separator)`
  > separator(구분자)를 포함하여 문자열 리턴

```js
let words = "hi hello ryulurala".split(" ");
console.log(words); // ["hi", "hello", "ryulurala"]

words.join("-"); // "hi-hello-ryulurala"
```

### 문자열 교체

- `str.replace(oldString, newString)`
  > oldString을 newString으로 교체
- `str.replace(regExp)`
  > regExp(정규식)으로 교체  
  > `g`: global(전역으로)  
  > `i`: ignore(대소문자 구별하지 않음)  
  > `\(백슬래시)`: 특수문자를 Escape 처리하여 문자 그대로로 인식

```js
let str = "hi hello ryulurala";
str.replace("hello", "bye"); // "hi bye ryulurala"

// 정규표현식(Regular Expression)
str.replace(/\./gi, ","); // '.'을 ','로 치환
str.replace(/[a-z]/gi, "A"); // 'a' 부터 'z'까지 대소문자 구별없이 A로 치환
str.replace(/[abc]/gi, ""); // 'a', 'b', 'c'를 찾아 문자열 내에 제거
str.replace(/[^abc]/gi, ""); // 'a', 'b', 'c'를 제외한 나머지 제거
str.replace(/\s/gi, ""); // 문자열 내에 모든 공백 제거
```

### Regular Expression(정규 표현식)

```js
const expression = "100*300+100-400/500";
expression.split(/[+-*/]/g); // ["100", "*", "300", "+", "100", "-" "400", "/", "500"]
```

---
