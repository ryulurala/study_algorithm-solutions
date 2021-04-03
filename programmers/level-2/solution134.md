---
title: "게임 맵 최단거리"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-04-03"
---

## 문제 링크

[게임 맵 최단거리](https://programmers.co.kr/learn/courses/30/lessons/1844)

### C++

```cpp
#include <vector>
#include <queue>
#include <iostream>

using namespace std;

bool isValid(vector<vector<int> >& maps, int row, int col){
    int n = maps.size();
    int m = maps[0].size();
    if(row < 0 || row >= n) return false;
    if(col < 0 || col >= m) return false;
    if(maps[row][col] == 0) return false;

    return true;
}

bool isLowestCost(vector<vector<int> >& costs, int row, int col, int cost){
    if(costs[row][col] == 0 || cost < costs[row][col]){
        costs[row][col] = cost;
        return true;
    }

    return false;
}

bool hasArrived(vector<vector<int> >& costs, int row, int col, int cost){
    int n = costs.size();
    int m = costs[0].size();
    if(row < n-1 || col < m-1) return false;

    if(cost < costs[n-1][m-1])
        costs[n-1][m-1] = cost;

    return true;
}

int solution(vector<vector<int> > maps) {
    int answer = 0;

    int n = maps.size();
    int m = maps[0].size();

    // 상, 우, 하, 좌
    int rowDir[] = {-1, 0, 1, 0};
    int colDir[] = {0, 1, 0, -1};

    vector<vector<int> > costs(maps.size(), vector<int>(maps[0].size(), 0));
    queue<pair<pair<int, int>, int> > q;
    q.push({{0, 0}, 1});
    while(!q.empty()){
        int r = q.front().first.first;
        int c = q.front().first.second;
        int cost = q.front().second;
        q.pop();

        // 올바른 길인지
        if(isValid(maps, r, c) == false) continue;
        // 제일 적은 비용인지
        if(isLowestCost(costs, r, c, cost) == false) continue;
        // 도착했는지
        if(hasArrived(costs, r, c, cost) == true) continue;

        // 4 방향 push
        for(int i=0; i<4; i++){
            q.push({{r+rowDir[i], c+colDir[i]}, cost+1});
        }
    }

    // answer
    answer = costs[n-1][m-1]==0 ? -1 : costs[n-1][m-1];

    return answer;
}
```

### JavaScript

```js
function solution(maps) {
  var answer = 0;

  const n = maps.length;
  const m = maps[0].length;

  class Node {
    constructor(row, col, cost) {
      this.row = row;
      this.col = col;
      this.cost = cost;
    }
  }

  // 상, 우, 하, 좌
  const rowDir = [-1, 0, 1, 0];
  const colDir = [0, 1, 0, -1];

  const queue = [];
  const costs = Array.from({ length: n }, () =>
    Array.from({ length: m }, () => 0)
  );
  queue.push(new Node(0, 0, 1));
  while (queue.length > 0) {
    const node = queue[0];
    queue.shift();

    const r = node.row;
    const c = node.col;
    const co = node.cost;

    // 유효한지
    if (r < 0 || r >= n) continue;
    else if (c < 0 || c >= m) continue;
    else if (maps[r][c] === 0) continue;

    // 적은 비용인지
    if (costs[r][c] > 0 && co >= costs[r][c]) continue;
    costs[r][c] = co;

    // 도착했는지
    if (r == n - 1 && c == m - 1) continue;

    // 4방향 push
    for (let i = 0; i < 4; i++) {
      queue.push(new Node(r + rowDir[i], c + colDir[i], co + 1));
    }
  }
  answer = costs[n - 1][m - 1] == 0 ? -1 : costs[n - 1][m - 1];

  return answer;
}
```
