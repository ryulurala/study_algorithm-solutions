---
title: "방문 길이"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-16"
---

## 문제 링크

[방문 길이](https://programmers.co.kr/learn/courses/30/lessons/49994)

### C++

```cpp
#include <string>
#include <set>

using namespace std;

int solution(string dirs) {
    int answer = 0;

    // 상, 우, 하, 좌
    int dir[4][2]={{0, 1}, {1, 0}, {0, -1}, {-1, 0}};

    set<pair<pair<int, int>, int> > edges;    // { {x, y}, dir }
    int sx=0, sy=0;
    for(char ch: dirs){
        int dirIndex;
        if(ch=='U') dirIndex=0;
        else if(ch=='R') dirIndex=1;
        else if(ch=='D') dirIndex=2;
        else if(ch=='L') dirIndex=3;

        // 목표 좌표
        int dx=sx+dir[dirIndex][0];
        int dy=sy+dir[dirIndex][1];

        if(dx<-5||dx>5||dy<-5||dy>5) continue;  // 범위 초과

        // 순방향 push
        edges.insert({{sx, sy}, dirIndex});

        // 역방향 push
        edges.insert({{dx, dy}, (dirIndex+2)%4});

        // next
        sx=dx;
        sy=dy;
    }
    answer=edges.size()/2;  // (순+역 edge 개수)/ 2

    return answer;
}
```

### JavaScript

```js
function solution(dirs) {
  var answer = 0;

  // 방향 벡터
  const dir = {
    U: [0, 1], // x, y, 상
    L: [-1, 0], // x, y, 좌
    D: [0, -1], // x, y, 하
    R: [1, 0], // x, y, 우
  };

  const edges = new Set();
  let sx = 0,
    sy = 0;
  dirs.split("").forEach((v) => {
    // 목표 지점 x, y
    const dx = sx + dir[v][0];
    const dy = sy + dir[v][1];

    if (dx >= -5 && dx <= 5 && dy >= -5 && dy <= 5) {
      const forward = [sx, sy, dx, dy].join(""); // 순방향
      const backward = [dx, dy, sx, sy].join(""); // 역방향

      // push: 중복 제거
      edges.add(forward);
      edges.add(backward);

      // next
      sx = dx;
      sy = dy;
    }
  });
  answer = edges.size / 2;

  return answer;
}
```
