---
title: "예산"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[예산](https://programmers.co.kr/learn/courses/30/lessons/12982)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> d, int budget) {
    int answer = 0;

    sort(d.begin(), d.end());

    for(int i=0; i<d.size(); i++){
        budget -= d[i];
        if(budget < 0) break;
        answer++;
    }

    return answer;
}
```

### JavaScript

```js
function solution(d, budget) {
  var answer = 0;

  d.sort((a, b) => {
    if (a < b) return -1;
    return 1;
  }).some((value) => {
    budget -= value;
    if (budget < 0) return true;
    answer++;
  });

  return answer;
}
```
