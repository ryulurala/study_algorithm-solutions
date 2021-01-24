---
title: "실패율"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[실패율](https://programmers.co.kr/learn/courses/30/lessons/42889)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

// 실패율 = 스테이지 클리어 못한 플레이 수 / 스테이지 도달한 플레이어 수

bool cmp(pair<int, float> a, pair<int, float> b){
    if(a.second == b.second) return a.first < b.first;  // 인덱스 작은 것부터
    return a.second > b.second;     // 실패율 큰 것부터
}

vector<int> solution(int N, vector<int> stages) {
    vector<int> answer;

    vector<int> players(N+2, 0);      // 현재 스테이지 플레이어 수
    vector<pair<int, float>> stage_fails;   // 스테이지_실패율
    int total = stages.size();  // 총 플레이어 수

    for(int player: stages) players[player]++;    // 중복 없이 증가

    for(int i=1; i<=N; i++){
        float fails = total!=0 ? (float) players[i]/total : 0;
        stage_fails.push_back(make_pair(i, fails)); // 스테이지, 실패율 push
        total -= players[i];
    }

    sort(stage_fails.begin(), stage_fails.end(), cmp);  // 정렬

    for(auto iter: stage_fails) answer.push_back(iter.first);

    return answer;
}
```

### JavaScript

```js
function solution(N, stages) {
  var answer = [];

  let totalPlayers = stages.length; // 모든 플레이어 수 증감
  const stagePlayers = Array.from({ length: N + 2 }, () => 0); // 현재 도전 중인 스테이지 초기화
  answer = Array.from({ length: N }, (value, index) => index + 1);

  stages.some((value) => {
    stagePlayers[value]++; // 현재 스테이지 도달 플레이어 수 증가
  });
  const fails = stagePlayers.map((value, index) => {
    if (totalPlayers == 0) return 0;
    const ret = stagePlayers[index] / totalPlayers; // 실패율
    totalPlayers -= stagePlayers[index];
    return ret;
  });

  answer.sort((a, b) => {
    if (fails[a] === fails[b]) return a - b;
    // 인덱스 작은 것부터
    else return fails[b] - fails[a]; // 실패율 큰 것부터
  });

  return answer;
}
```
