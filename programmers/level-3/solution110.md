---
title: "입국심사"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-06"
---

## 문제 링크

[입국심사](https://programmers.co.kr/learn/courses/30/lessons/43238)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

long long solution(int n, vector<int> times) {
    long long answer = 0;

    stable_sort(times.begin(), times.end()); // 오름차순

    long long rightT=(long long)times.front()*n;
    long long leftT=1;
    while(leftT<=rightT){
        long long time=(rightT+leftT)/2;
        long long person=0;
        for(int t: times) person+=(time/t); // 심사 가능한 인원
        if(person>=n) {
            // 모두 심사 가능한 경우
            rightT=time-1;
            answer=time;
        }
        else{
            // 불가능한 경우
            leftT=time+1;
            answer=time+1;
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(n, times) {
  var answer = 0;

  times.sort((a, b) => a - b); // 오름차순
  let rightT = times[0] * n;
  let leftT = 1;

  while (leftT <= rightT) {
    let time = parseInt((rightT + leftT) / 2);
    const person = times.reduce((sum, t) => sum + parseInt(time / t), 0); // 심사 인원
    if (person >= n) {
      // n명 이상 심사 가능
      rightT = time - 1;
      answer = time; // 가능하므로
    } else {
      // 불가능
      leftT = time + 1;
      answer = time + 1; // 불가능하므로 하나 추가
    }
  }

  return answer;
}
```
