---
title: "2 x n 타일링"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-03"
---

## 문제 링크

[2 x n 타일링](https://programmers.co.kr/learn/courses/30/lessons/12900)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

int solution(int n) {
    int answer = 0;

    vector<int> tile(n+1);
    tile[1]=1;
    tile[2]=2;
    for(int i=3; i<=n; i++){
        tile[i]=tile[i-2]+tile[i-1];
        tile[i]%=1000000007;
    }
    answer=tile[n];

    return answer;
}
```

### JavaScript

```js
function solution(n) {
  var answer = 0;

  const tile = Array.from({ length: n + 1 }, () => 0);
  tile[1] = 1;
  tile[2] = 2;
  for (let i = 3; i <= n; i++) {
    tile[i] = tile[i - 2] + tile[i - 1];
    tile[i] %= 1000000007;
  }
  answer = tile[n];

  return answer;
}
```
