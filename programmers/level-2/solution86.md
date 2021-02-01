---
title: "예상 대진표"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-01"
---

## 문제 링크

[예상 대진표](https://programmers.co.kr/learn/courses/30/lessons/12985)

### C++

```cpp
#include <iostream>
#include <cmath>

using namespace std;

int solution(int n, int a, int b) {
    int answer = 0;

    while(abs(a-b)>=1){
        answer++;
        a=a&1?(a+1)>>1:a>>1;
        b=b&1?(b+1)>>1:b>>1;
    }

    return answer;
}
```

### JavaScript

```js
function solution(n, a, b) {
  var answer = 0;

  while (Math.abs(a - b) >= 1) {
    answer++;
    a = a & 1 ? (a + 1) >> 1 : a >> 1;
    b = b & 1 ? (b + 1) >> 1 : b >> 1;
  }

  return answer;
}
```
