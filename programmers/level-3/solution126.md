---
title: "기지국 설치"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-20"
---

## 문제 링크

[기지국 설치](https://programmers.co.kr/learn/courses/30/lessons/12979)

### C++

```cpp
#include <iostream>
#include <vector>

using namespace std;

int solution(int n, vector<int> stations, int w) {
    int answer = 0;

    int from=1; // ~부터
    int range=2*w+1;    // 범위

    for(int station: stations){
        int to=station-w;   // ~전까지

        if(to>from){
            int count=to-from;      // 전파 닿지 않는 개수

            // 기지국 개수 추가
            answer += count/range;
            answer += count%range!=0?1:0;
        }
        from=station+w+1;   // for. next
    }
    if(from<=n){
        // 아직 남음
        int to=n+1;   // ~전까지
        int count=to-from;

        // 기지국 개수 추가
        answer += count/range;
        answer += count%range!=0?1:0;
    }

    return answer;
}
```

### JavaScript

```js
function solution(n, stations, w) {
  var answer = 0;

  const range = 2 * w + 1; // 범위
  let from = 1;
  stations.forEach((station) => {
    const to = station - w; // ~전까지
    if (to > from) {
      const count = to - from; // 전파 닿지 않는 갯수
      answer += Math.ceil(count / range); // 기지국 개수
    }
    from = station + w + 1; // for. next
  });
  if (from <= n) {
    // 아직 남아있을 때
    const to = n + 1; // ~전까지
    const count = to - from; // 전파 닿지 않는 갯수
    answer += Math.ceil(count / range); // 기지국 개수
  }

  return answer;
}
```
