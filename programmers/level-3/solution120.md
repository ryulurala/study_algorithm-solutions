---
title: "배달"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-15"
---

## 문제 링크

[배달](https://programmers.co.kr/learn/courses/30/lessons/12978)

### C++

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

int solution(int N, vector<vector<int> > road, int K) {
    int answer = 0;

    // init
    vector<pair<int, int> > graph[N+1]; // 걸리는 시간_마을(정점)
    for(auto vec: road){
        int t1=vec[0];
        int t2=vec[1];
        int h=vec[2];
        graph[t1].push_back({h, t2});
        graph[t2].push_back({h, t1});
    }

    // dijkstra
    vector<int> hours(N+1, 500001);  // 1번 마을로부터 각 마을까지 걸리는 시간들
    priority_queue<pair<int, int> > pq;

    pq.push({0, 1});  // hour:0, start: 1
    hours[1]=0;
    while(!pq.empty()){
        int hour=(-pq.top().first); // 1번 마을에서 온 시간
        int here=pq.top().second;   // 현재 마을
        pq.pop();

        if(hours[here]<hour) continue;  // 이미 최소

        for(auto p: graph[here]){
            // 인접한 마을 검사
            int nextHour=hour+p.first;  // next마을을 거쳐가는 시간
            int there=p.second;  // next 마을

            if(nextHour<hours[there]){
                // 거쳐서 간 시간이 짧으면
                hours[there]=nextHour;
                pq.push({-nextHour, there});
            }
        }
    }

    // 가능한 경우 모두 검사(자신 포함)
    for(int i=1; i<=N; i++){
        if(hours[i]<=K) answer++;
    }

    return answer;
}
```

### JavaScript

```js
function solution(N, road, K) {
  var answer = 0;

  // init
  const graph = Array.from({ length: N + 1 }, () => []);
  road.forEach((arr) => {
    const here = arr[0];
    const there = arr[1];
    const hour = arr[2];

    // 연결
    graph[here].push([hour, there]);
    graph[there].push([hour, here]);
  });

  const hours = Array.from({ length: N + 1 }, () => 500001); // 1번 마을로부터 거리
  const pq = []; // priority_queue

  hours[1] = 0;
  pq.push([0, 1]); // hour: 0, start: 1
  while (pq.length !== 0) {
    const pqHours = pq.map((v) => v[0]);
    const minIndex = pqHours.indexOf(Math.min(...pqHours));

    const hour = pq[minIndex][0]; // 1번 마을로부터 걸리는 시간
    const here = pq[minIndex][1]; // 현재 마을

    pq.splice(minIndex, 1); // pop

    if (hours[here] < hour) continue; // 이미 최소

    for (const arr of graph[here]) {
      // 연결된 마을로부터
      const nextHour = hour + arr[0]; // 다음 마을까지 현재 마을 거쳐서 가는 거리
      const there = arr[1]; // 다음 마을

      if (hours[there] > nextHour) {
        hours[there] = nextHour;
        pq.push([nextHour, there]);
      }
    }
  }

  for (let i = 1; i <= N; i++) {
    if (hours[i] <= K) answer++;
  }

  return answer;
}
```
