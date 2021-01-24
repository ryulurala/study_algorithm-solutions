---
title: "x만큼 간격이 있는 n개의 숫자"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[x만큼 간격이 있는 n개의 숫자](https://programmers.co.kr/learn/courses/30/lessons/12954)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

vector<long long> solution(int x, int n) {
    vector<long long> answer;

    for(int i=1; i<=n; i++){
        answer.push_back(x*i);
    }

    return answer;
}
```

### JavaScript

```js
function solution(x, n) {
  var answer = [];

  for (let i = 1; i <= n; i++) {
    answer.push(x * i);
  }

  return answer;
}
```
