---
title: "짝수와 홀수"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-20"
---

## 문제 링크

[짝수와 홀수](https://programmers.co.kr/learn/courses/30/lessons/12937)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

string solution(int num) {
    string answer = "";

    answer = num & 1 ? "Odd" : "Even";

    return answer;
}
```

### JavaScript

```js
function solution(num) {
  var answer = "";

  answer = num & 1 ? "Odd" : "Even";

  return answer;
}
```
