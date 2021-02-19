---
title: "야근 지수"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-20"
---

## 문제 링크

[야근 지수](https://programmers.co.kr/learn/courses/30/lessons/12927)

### C++

```cpp
#include <string>
#include <vector>
#include <queue>

using namespace std;

long long solution(int n, vector<int> works) {
    long long answer = 0;

    // init
    priority_queue<int> pq(works.begin(), works.end());

    while(n-->0){
        int work=pq.top();
        if(work==0) return 0;   // 모든 일이 끝남
        pq.pop();
        pq.push(work-1);    // 작업량 1 감소
    }

    while(!pq.empty()){
        int work=pq.top();
        pq.pop();
        answer += work*work;
    }

    return answer;
}
```

### JavaScript

```js
function solution(n, works) {
  var answer = 0;

  works.sort((a, b) => b - a); // 내림차순

  let max = works[0]; // 최대값
  while (n > 0) {
    if (max === 0) return 0; // 일이 끝남

    for (let i = 0; i < works.length; i++) {
      if (max !== works[i] || n === 0) break;
      works[i]--;
      n--;
    }
    max--; // 최댓값 갱신
  }
  answer = works.reduce((p, c) => p + c * c, 0); // 모든 합

  return answer;
}
```
