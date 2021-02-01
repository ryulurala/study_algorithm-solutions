---
title: "점프와 순간 이동"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-01"
---

## 문제 링크

[점프와 순간 이동](https://programmers.co.kr/learn/courses/30/lessons/12980)

### C++

```cpp
#include <iostream>

using namespace std;

int solution(int n) {
    int ans = 0;

    while(n>0){
        if(n&1) ans++;
        n>>=1;
    }

    return ans;
}
```

### JavaScript

```js
function solution(n) {
  var ans = 0;

  while (n > 0) {
    if (n & 1) ans++;
    n >>>= 1;
  }

  return ans;
}
```
