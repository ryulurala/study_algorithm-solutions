---
title: "섬 연결하기"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-05"
---

## 문제 링크

[섬 연결하기](https://programmers.co.kr/learn/courses/30/lessons/42861)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <map>
#include <iostream>

using namespace std;

bool cmp(vector<int> a, vector<int> b){
    return a[2]<b[2];
}

int findRoot(map<int, int>& root, int num){
    if(root[num]==num) return num;
    else return root[num]=findRoot(root, root[num]);
}

int solution(int n, vector<vector<int>> costs) {
    int answer = 0;

    // 비용 기준 오름차순 정렬
    stable_sort(costs.begin(), costs.end(), cmp);

    // init
    map<int, int> root;
    for(int i=0; i<n; i++) root[i]=i;

    for(auto e: costs){
        int root1=findRoot(root, e[0]);
        int root2=findRoot(root, e[1]);
        if(root1!=root2){
            // root가 다르면
            answer+=e[2];
            // 루트 갱신
            root[root2]=root1;
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(n, costs) {
  var answer = 0;

  const findRoot = (root, num) => {
    if (root[num] === num) return num;
    else return (root[num] = findRoot(root, root[num]));
  };

  // 비용 기준으로 오름차순 정렬
  costs.sort((a, b) => a[2] - b[2]);

  const root = [];
  for (let i = 0; i < n; i++) root.push(i);

  for (const arr of costs) {
    const root1 = findRoot(root, arr[0]);
    const root2 = findRoot(root, arr[1]);
    if (root1 !== root2) {
      // 루트가 다를 경우, 연결(크루스칼)
      answer += arr[2];
      root[root2] = root1;
    }
  }

  return answer;
}
```
