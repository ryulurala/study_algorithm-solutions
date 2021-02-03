---
title: "추석 트래픽"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-03"
---

## 문제 링크

[추석 트래픽](https://programmers.co.kr/learn/courses/30/lessons/17676)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

int solution(vector<string> lines) {
    int answer = 0;

    vector<float> section; // 구간
    vector<pair<float, float>> start_end;    // 처리 시작~끝

    // 문자열 파싱
    for(string line: lines){
        float hh=stof(line.substr(11, 2));
        float mm=stof(line.substr(14, 2));
        float ss=stof(line.substr(17, 6));
        float tt=stof(line.substr(24));
        ss+=hh*3600+mm*60;
        section.push_back(ss);
        start_end.push_back(make_pair(ss-tt+0.001f, ss));
    }

    // 구간 탐색
    for(float p: section){
        float left=p; // 구간 시작
        float right=p+0.999f;   // 구간 끝
        int count=0;
        for(auto e: start_end){
            float start=e.first;
            float end=e.second;
            if(start<=right&&end>=left) count++;    // 구간에 포함
        }
        answer=max(answer, count);
    }

    return answer;
}
```

### JavaScript

```js
function solution(lines) {
  var answer = 0;

  const section = []; // 구간 시작

  // 문자열 파싱
  const start_end = lines.map((line) => {
    line = line.split(" ");
    const time = line[1].split(":").map((v) => parseFloat(v));
    const end = (time[0] * 3600 + time[1] * 60 + time[2]).toFixed(3);
    const second = parseFloat(line[2]).toFixed(3);
    section.push(+end);
    return [+end - second + 0.001, +end];
  });

  // 구간 탐색
  section.forEach((left) => {
    const right = (+left + 0.999).toFixed(3);
    let count = 0;
    for (const [start, end] of start_end) {
      if (start <= right && end >= left) count++;
    }
    answer = Math.max(answer, count);
  });

  return answer;
}
```
