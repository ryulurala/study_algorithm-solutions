---
title: "조이스틱"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-25"
---

## 문제 링크

[조이스틱](https://programmers.co.kr/learn/courses/30/lessons/42860)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(string name) {
    int answer = 0;

    vector<int> noA;
    for(int i=0; i<name.length(); i++){
        if(name[i]!='A') {
            noA.push_back(i);   // 인덱스 push
        }
    }

    int current=0;
    int length=name.length();
    while(!noA.empty()){
        // 좌, 우 커서 움직임
        // 정방향
        int rightDist=current>noA.front() ?
            noA.front()+length-current : noA.front()-current;
        // 역방향
        int leftDist=current>noA.back() ?
            current-noA.back() : current+length-noA.back();

        if(leftDist<rightDist){
            // 왼쪽이 더 가까움
            current=noA.back();
            noA.pop_back();       // back 제거
            answer+=leftDist;
        }
        else{
            // 오른쪽이 더 가까움
            current=noA.front();
            noA.erase(noA.begin()); // front 제거
            answer+=rightDist;
        }

        // 상, 하 커서 움직임
        answer+=min(name[current]-'A', 'Z'-name[current]+1);
    }

    return answer;
}
```

### JavaScript

```js
function solution(name) {
  var answer = 0;

  let noA = [];
  const LUT = [
    0,
    1,
    2,
    3,
    4,
    5,
    6,
    7,
    8,
    9,
    10,
    11,
    12,
    13,
    12,
    11,
    10,
    9,
    8,
    7,
    6,
    5,
    4,
    3,
    2,
    1,
  ];
  for (let i = 0; i < name.length; i++) {
    if (name[i] === "A") continue;
    noA.push(i); // index push
  }

  let i = 0; // 좌, 우 커서
  const len = name.length;
  while (noA.length > 0) {
    // 정방향
    const rightDist = i > noA[0] ? noA[0] + len - i : noA[0] - i;
    // 역방향
    const leftDist =
      i > noA[noA.length - 1]
        ? i - noA[noA.length - 1]
        : i + len - noA[noA.length - 1];

    if (leftDist < rightDist) {
      // 왼쪽이 더 가깝다
      i = noA[noA.length - 1];
      noA.pop();
      answer += leftDist;
    } else {
      // 오른쪽이 더 가깝다
      i = noA[0];
      noA.shift();
      answer += rightDist;
    }

    // 상, 하 커서
    answer += LUT[name[i].charCodeAt() - "A".charCodeAt()];
  }

  return answer;
}
```
