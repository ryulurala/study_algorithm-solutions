---
title: "내적"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[내적](https://programmers.co.kr/learn/courses/30/lessons/70128)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

int solution(vector<int> a, vector<int> b) {
    int answer = 0;

    for(int i=0; i<a.size(); i++){
        answer += a[i] * b[i];
    }

    return answer;
}
```

### JavaScript

```js
function solution(a, b) {
  var answer = 0;

  for (let i = 0; i < a.length; i++) {
    answer += a[i] * b[i];
  }

  return answer;
}
```
