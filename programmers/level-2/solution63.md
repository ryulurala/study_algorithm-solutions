---
title: "위장"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-28"
---

## 문제 링크

[위장](https://programmers.co.kr/learn/courses/30/lessons/42578)

### C++

```cpp
#include <string>
#include <vector>
#include <map>

using namespace std;

int solution(vector<vector<string>> clothes) {
    int answer = 0;

    map<string, int> cloth_count;   // 종류당 개수

    for(auto e: clothes){
        cloth_count[e[1]]++;
    }

    answer=1;
    for(auto e: cloth_count){
        answer*=(e.second+1);
    }

    return answer-1;
}
```

### JavaScript

```js
function solution(clothes) {
  var answer = 0;

  const cloth_count = new Map(); // 종류별 개수

  for (const cloth of clothes) {
    if (!cloth_count.has(cloth[1])) {
      cloth_count.set(cloth[1], 1);
    } else {
      const count = cloth_count.get(cloth[1]);
      cloth_count.set(cloth[1], count + 1);
    }
  }

  answer = 1;
  for (const e of cloth_count) {
    answer *= e[1] + 1;
  }

  return answer - 1;
}
```
