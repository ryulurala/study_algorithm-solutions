---
title: "줄 서는 방법"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-16"
---

## 문제 링크

[줄 서는 방법](https://programmers.co.kr/learn/courses/30/lessons/12936)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

vector<int> solution(int n, long long k) {
    vector<int> answer;

    // init
    vector<int> remains;
    long long fac=1;
    for(int i=1; i<=n; i++) {
        remains.push_back(i);
        fac*=i;
    }

    k--;    // for. indexing, k-1
    for(int i=0; i<n; i++){
        fac/=(n-i);    // (n-1)!, (n-2)!, ..., 1!
        answer.push_back(remains[k/fac]);
        remains.erase(remains.begin()+(k/fac));   // 요소 하나씩 삭제
        k%=fac;
    }

    return answer;
}
```

### JavaScript

```js
function solution(n, k) {
  var answer = [];

  // init
  const remains = Array.from({ length: n }, (v, i) => i + 1); // [1, 2, ..., n]
  let fac = remains.reduce((prev, curr) => prev * curr, 1); // n!

  k--; // for. indexing
  for (let i = 0; i < n; i++) {
    fac /= n - i; // ex. (n-1)!, (n-2)!, ..., 1!
    const index = parseInt(k / fac);
    answer.push(remains[index]);
    remains.splice(index, 1); // erase
    k %= fac;
  }

  return answer;
}
```
