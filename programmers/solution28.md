---
title: "정수 제곱근 판별"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[정수 제곱근 판별](https://programmers.co.kr/learn/courses/30/lessons/12934)

### C++

```cpp
#include <string>
#include <vector>
#include <cmath>

using namespace std;

long long solution(long long n) {
    long long answer = 0;

    if((long long)sqrt(n) == sqrt(n)) {
        answer = pow(sqrt(n)+1, 2);
    }
    else {
        answer = -1;
    }

    return answer;
}
```

### JavaScript

```js
function solution(n) {
  var answer = 0;

  if (Math.sqrt(n) === parseInt(Math.sqrt(n))) {
    answer = Math.pow(Math.sqrt(n) + 1, 2);
  } else {
    answer = -1;
  }

  return answer;
}
```
