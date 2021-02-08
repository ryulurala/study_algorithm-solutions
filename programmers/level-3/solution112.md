---
title: "순위"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-08"
---

## 문제 링크

[순위](https://programmers.co.kr/learn/courses/30/lessons/49191)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

int solution(int n, vector<vector<int>> results) {
    int answer = 0;

    // init
    vector<vector<bool>> record(n+1, vector<bool>(n+1, false));
    for(auto r: results) record[r[0]][r[1]]=true;   // r[0]이 r[1]을 이긴다.

    for(int k=1; k<=n; k++){
        for(int i=1; i<=n; i++){
            for(int j=1; j<=n; j++){
                if(record[i][k]&&record[k][j]){
                    // i가 k를 이기고 k가 j를 이길 경우
                    record[i][j]=true;  // i도 j를 이긴다.
                }
            }
        }
    }

    for(int i=1; i<=n; i++){
        int count=0;
        for(int j=1; j<=n; j++){
            if(record[i][j]||record[j][i]) count++; // i가 j를 이기거나 j에게 졌을 경우
        }
        if(count==n-1) answer++;
    }

    return answer;
}
```

### JavaScript

```js
function solution(n, results) {
  var answer = 0;

  // init
  const record = Array.from({ length: n + 1 }, () =>
    Array.from({ length: n + 1 }, () => false)
  );

  results.forEach((v) => {
    // v[0]이 v[1]을 이긴다
    record[v[0]][v[1]] = true;
  });

  for (let k = 1; k <= n; k++) {
    for (let i = 1; i <= n; i++) {
      for (let j = 1; j <= n; j++) {
        if (record[i][k] && record[k][j]) {
          // i가 k를 이기고 k가 j를 이기면
          record[i][j] = true; // i가 j를 이긴다.
        }
      }
    }
  }

  for (let i = 1; i <= n; i++) {
    let cnt = 0;
    for (let j = 1; j <= n; j++) {
      if (record[i][j] || record[j][i]) cnt++;
    }
    if (cnt === n - 1) answer++; // i가 모든 경기를 한 것과 같을 때
  }

  return answer;
}
```
