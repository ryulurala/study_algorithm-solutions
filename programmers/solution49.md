---
title: "프린터"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-2]
toc: true
toc_sticky: true
---

## 문제 링크

[프린터](https://programmers.co.kr/learn/courses/30/lessons/42587)

### C++

```cpp
#include <string>
#include <vector>
#include <queue>
#include <algorithm>

using namespace std;

int solution(vector<int> priorities, int location) {
    int answer = 0;

    vector<pair<int, int>> v;   // 저장용
    queue<pair<int, int>> q;    // 순서목록
    for(int i=0; i<priorities.size(); i++){
        q.push(make_pair(i, priorities[i]));
    }

    sort(priorities.rbegin(), priorities.rend());   // 내림차순

    for(int i=0; i<priorities.size(); ){
        pair<int, int> cur = q.front();
        q.pop();
        if(cur.second != priorities[i]) q.push(cur);
        else {
            v.push_back(cur);
            i++;
        }
    }

    for(int i=0; i<v.size(); i++){
        if(v[i].first != location) continue;
        answer = i+1;
    }

    return answer;
}
```

### JavaScript

```js
function solution(priorities, location) {
  var answer = 0;

  let vector = []; // 저장용
  const queue = priorities.map((value, index) => {
    // 큐 초기화
    return [index, value];
  });
  priorities.sort((a, b) => b - a);

  for (let i = 0; i < priorities.length; ) {
    const cur = queue.shift();
    if (cur[1] !== priorities[i]) {
      queue.push(cur);
    } else {
      vector.push(cur);
      i++;
    }
  }

  vector.some((value, index) => {
    if (value[0] === location) {
      answer = index + 1;
      return true;
    }
  });

  return answer;
}
```
