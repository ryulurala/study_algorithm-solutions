---
title: "정수 내림차순으로 배치하기"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[정수 내림차순으로 배치하기](https://programmers.co.kr/learn/courses/30/lessons/12933)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

long long solution(long long n) {
    long long answer = 0;

    string str = to_string(n);  // string 변환
    sort(str.rbegin(), str.rend()); // 사전 반대 정렬
    answer = stoll(str);    // long long 변환

    return answer;
}
```

### JavaScript

```js
function solution(n) {
  var answer = 0;

  answer = n
    .toString()
    .split("")
    .sort((a, b) => (a > b ? -1 : 1))
    .join("");

  return +answer;
}
```
