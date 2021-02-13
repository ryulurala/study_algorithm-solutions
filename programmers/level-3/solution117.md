---
title: "멀리 뛰기"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-13"
---

## 문제 링크

[멀리 뛰기](https://programmers.co.kr/learn/courses/30/lessons/12914)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

long long solution(int n) {
    long long answer = 0;

    vector<long long> counts(n+1);
    counts[1]=1;
    counts[2]=2;
    for(int i=3; i<=n; i++){
        counts[i]=counts[i-1]+counts[i-2];
        counts[i]%=1234567;     // 미리 나누기
    }
    answer=counts[n];

    return answer;
}
```

### JavaScript

```js
function solution(n) {
  var answer = 0;

  const counts = Array.from({ length: n + 1 }, () => 0);
  counts[1] = 1;
  counts[2] = 2;
  for (let i = 3; i <= n; i++) {
    counts[i] = counts[i - 1] + counts[i - 2];
    counts[i] %= 1234567; // 미리 나누기
  }
  answer = counts[n];

  return answer;
}
```
