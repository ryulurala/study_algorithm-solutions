---
title: "H-Index"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-28"
---

## 문제 링크

[H-Index](https://programmers.co.kr/learn/courses/30/lessons/42747)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> citations) {
    int answer = citations.size();  // 논문 n편

    stable_sort(citations.begin(), citations.end());    // 오름차순 정렬

    for(int citation: citations){
        if(answer>citation) answer--;
    }

    return answer;
}
```

### JavaScript

```js
function solution(citations) {
  var answer = citations.length; // 논문 n편

  citations.sort();
  citations.some((v) => {
    if (answer > v) answer--;
  });

  return answer;
}
```
