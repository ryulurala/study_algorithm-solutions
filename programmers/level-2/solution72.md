---
title: "땅따먹기"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-30"
---

## 문제 링크

[땅따먹기](https://programmers.co.kr/learn/courses/30/lessons/12913)

### C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<vector<int>> land) {
    int answer = 0;

    for(int i=1; i<land.size(); i++){
        // 현재 열을 제외한 이전 행의 최댓값 + 현재 발판
        land[i][0] += max(land[i-1][1], max(land[i-1][2], land[i-1][3]));
        land[i][1] += max(land[i-1][0], max(land[i-1][2], land[i-1][3]));
        land[i][2] += max(land[i-1][0], max(land[i-1][1], land[i-1][3]));
        land[i][3] += max(land[i-1][0], max(land[i-1][1], land[i-1][2]));
    }

    // 마지막 행에서 최댓값 추출
    answer=*max_element(land.back().begin(), land.back().end());

    return answer;
}
```

### JavaScript

```js
function solution(land) {
  var answer = 0;

  for (let i = 1; i < land.length; i++) {
    // 현재 열을 제외한 이전 행의 최댓값 + 현재 발판
    land[i][0] += Math.max(land[i - 1][1], land[i - 1][2], land[i - 1][3]);
    land[i][1] += Math.max(land[i - 1][0], land[i - 1][2], land[i - 1][3]);
    land[i][2] += Math.max(land[i - 1][0], land[i - 1][1], land[i - 1][3]);
    land[i][3] += Math.max(land[i - 1][0], land[i - 1][1], land[i - 1][2]);
  }

  // 마지막 행의 최댓값
  const back = land.length - 1;
  answer = Math.max(land[back][0], land[back][1], land[back][2], land[back][3]);

  return answer;
}
```
