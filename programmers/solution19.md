---
title: "문자열을 정수로 바꾸기"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[문자열을 정수로 바꾸기](https://programmers.co.kr/learn/courses/30/lessons/12925)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

int solution(string s) {
    int answer = 0;

    answer = stoi(s);

    return answer;
}
```

### JavaScript

```js
function solution(s) {
  var answer = 0;

  answer = s * 1;

  return answer;
}
```
