---
title: "네트워크"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-04"
---

## 문제 링크

[네트워크](https://programmers.co.kr/learn/courses/30/lessons/43162)

### C++

```cpp
#include <string>
#include <vector>
#include <map>

using namespace std;

int findRoot(map<int, int>& root, int num){
    if(root[num]==num) return num;
    else return findRoot(root, root[num]);    // 제일 높은 루트 저장
}

int solution(int n, vector<vector<int>> computers) {
    int answer = 0;

    map<int, int> root;
    for(int i=0; i<n; i++) root[i]=i;

    for(int i=0; i<n-1; i++){
        for(int j=i+1; j<n; j++){
            if(computers[i][j]==0) continue;
            int rootI=findRoot(root, i);
            int rootJ=findRoot(root, j);

            // root가 작은 걸로 갱신
            root[max(rootI, rootJ)]=min(rootI, rootJ);
        }
    }

    // 갯수 세기
    for(int i=0; i<n; i++){
        if(i==findRoot(root, i)) answer++;
    }

    return answer;
}
```

### JavaScript

```js
function solution(n, computers) {
  var answer = 0;

  const dfsGo = (index, visited) => {
    visited[index] = true; // 방문

    for (let j = 0; j < n; j++) {
      if (!visited[j] && computers[index][j]) {
        // 방문안하고 연결됐을 경우
        dfsGo(j, visited);
      }
    }
  };

  const visited = Array.from({ length: n }, () => false);

  for (let i = 0; i < n; i++) {
    if (!visited[i]) {
      // 방문안했을 경우
      answer++;
      dfsGo(i, visited);
    }
  }

  return answer;
}
```
