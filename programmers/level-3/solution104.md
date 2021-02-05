---
title: "단속카메라"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-05"
---

## 문제 링크

[단속카메라](https://programmers.co.kr/learn/courses/30/lessons/42884)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

bool cmp(vector<int> a, vector<int> b){
    return a[1]<b[1];
}

int solution(vector<vector<int>> routes) {
    int answer = 1;

    // 나간 시점을 기준으로 정렬
    stable_sort(routes.begin(), routes.end(), cmp);

    int idx=0;
    int end=routes[idx++][1];   // 카메라 설치 지점
    while(idx<routes.size()){
        int start=routes[idx][0];
        if(start>end){
            // 진입이 카메라 설치할 지점보다 작을 경우
            answer++;
            end=routes[idx][1];
        }
        idx++;
    }

    return answer;
}
```

### JavaScript

```js
function solution(routes) {
  var answer = 0;

  routes.sort((a, b) => a[1] - b[1]); // 나간 시점 기준 오름차순

  let end = -30001;
  routes.forEach((v) => {
    const start = v[0];
    if (start > end) {
      // 카메라 설치 지점보다 진입 시점이 클 때
      answer++;
      end = v[1];
    }
  });

  return answer;
}
```
