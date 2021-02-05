---
title: "가장 먼 노드"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-05"
---

## 문제 링크

[가장 먼 노드](https://programmers.co.kr/learn/courses/30/lessons/49189)

### C++

```cpp
#include <string>
#include <vector>
#include <map>
#include <queue>
#include <algorithm>

using namespace std;

int solution(int n, vector<vector<int>> edge) {
    int answer = 0;

    // init
    map<int, vector<int>> node;
    for(int i=0; i<edge.size(); i++){
        node[edge[i][0]].push_back(edge[i][1]);
        node[edge[i][1]].push_back(edge[i][0]);
    }

    vector<bool> visited(n+1, false);   // 방문 여부
    vector<int> dist(n+1, 0);   // 거리
    queue<int> q;

    // 1 방문
    visited[1]=true;
    for(int i=0; i<node[1].size(); i++){
        visited[node[1][i]]=true;   // 방문 체크
        q.push(node[1][i]);
        dist[node[1][i]]=1;     // 1과의 거리: 1
    }

    // BFS
    while(!q.empty()){
        int front=q.front();
        q.pop();
        for(int i=0; i<node[front].size(); i++){
            if(!visited[node[front][i]]){
                visited[node[front][i]]=true;
                q.push(node[front][i]);
                dist[node[front][i]]=dist[front]+1;
            }
        }
    }

    // 거리 최대
    int maxDist=*max_element(dist.begin(), dist.end());
    for(int e: dist){
        if(e==maxDist) answer++;
    }

    return answer;
}
```

### JavaScript

```js
function solution(n, edge) {
  var answer = 0;

  const adjList = []; // 인접 리스트
  for (let i = 0; i < n + 1; i++) {
    adjList.push([]);
  }

  edge.forEach((v) => {
    const x = v[0];
    const y = v[1];
    adjList[x].push(y);
    adjList[y].push(x);
  });

  const queue = [];
  const dist = Array.from({ length: n + 1 }, () => 0);
  const visited = Array.from({ length: n + 1 }, () => false);

  // 1 방문
  visited[1] = true;
  for (let i = 0; i < adjList[1].length; i++) {
    const num = adjList[1][i];
    visited[num] = true;
    queue.push(num);
    dist[num] = 1;
  }

  // 나머지 방문(BFS)
  while (queue.length > 0) {
    const front = queue[0];
    queue.shift(); // pop
    for (let i = 0; i < adjList[front].length; i++) {
      const num = adjList[front][i];
      if (!visited[num]) {
        visited[num] = true;
        queue.push(num);
        dist[num] = dist[front] + 1;
      }
    }
  }

  // 가장 먼 노드
  const maxDist = Math.max(...dist);
  dist.forEach((v) => {
    if (v === maxDist) answer++;
  });

  return answer;
}
```
