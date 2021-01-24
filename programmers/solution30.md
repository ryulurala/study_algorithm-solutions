---
title: "짝수와 홀수"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
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
