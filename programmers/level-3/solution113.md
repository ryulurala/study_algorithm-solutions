---
title: "합승 택시 요금"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-08"
---

## 문제 링크

[합승 택시 요금](https://programmers.co.kr/learn/courses/30/lessons/72413)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

int solution(int n, int s, int a, int b, vector<vector<int>> fares) {
    int answer = 0;

    // init
    vector<vector<int> > graph(n+1, vector<int>(n+1, 100001*n) );
    for(auto v: fares){
        graph[v[0]][v[1]]=v[2];
        graph[v[1]][v[0]]=v[2];
    }

    // Floyd-Warshall
    for(int k=1; k<=n; k++){
        for(int i=1; i<=n; i++){
            for(int j=1; j<=n; j++){
                if(i==j) graph[i][j]=0;     // 출발 지점=도착지점
                // i에서 j로 가는 최소 요금 = "i에서 j 요금" or "i에서 k요금 + k에서 j요금"
                else graph[i][j]=min(graph[i][j], graph[i][k]+graph[k][j]);
            }
        }
    }

    answer=100001*n;   // Infinite
    for(int k=1; k<=n; k++){
        // s에서 k까지 + k에서 a까지 + k에서 b까지의 최소
        answer=min(answer, graph[s][k]+graph[k][a]+graph[k][b]);
    }

    return answer;
}
```

### JavaScript

```js
function solution(n, s, a, b, fares) {
  var answer = 0;

  // init
  const graph = Array.from({ length: n + 1 }, () =>
    Array.from({ length: n + 1 }, () => 100001 * n)
  );
  fares.forEach((v) => {
    graph[v[0]][v[1]] = v[2];
    graph[v[1]][v[0]] = v[2];
  });

  // Floyd-Warshall
  for (let k = 1; k <= n; k++) {
    for (let i = 1; i <= n; i++) {
      for (let j = 1; j <= n; j++) {
        if (i == j) graph[i][j] = 0;
        else graph[i][j] = Math.min(graph[i][j], graph[i][k] + graph[k][j]);
      }
    }
  }

  answer = 100001 * n; // Infinite
  for (let k = 1; k <= n; k++) {
    // s->k + k->a + k->b의 최소
    answer = Math.min(answer, graph[s][k] + graph[k][a] + graph[k][b]);
  }

  return answer;
}
```
