---
title: "기능개발"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-2]
toc: true
toc_sticky: true
---

## 문제 링크

[기능개발](https://programmers.co.kr/learn/courses/30/lessons/42586)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(vector<int> progresses, vector<int> speeds) {
    vector<int> answer;

    reverse(progresses.begin(), progresses.end());  // for. 스택으로 이용
    reverse(speeds.begin(), speeds.end());      // for. 스택으로 이용

    while(!progresses.empty()){
        int count = 0;      // 날짜 수
        int totalSize = progresses.size();  // 이전 크기값
        while(progresses.back()<100){
            progresses.back() += speeds.back();
            count++;    // 지난 날짜 수 증가
        }
        progresses.pop_back();
        speeds.pop_back();

        for(int i=0; i<progresses.size(); i++){
            progresses[i] += speeds[i]*count;   // 모든 진행도 갱신
        }
        while(!progresses.empty()){
            if(progresses.back()<100) break;
            progresses.pop_back();
            speeds.pop_back();
        }
        answer.push_back(totalSize-progresses.size());  // 배포한 횟수
    }


    return answer;
}
```

### JavaScript

```js
function solution(progresses, speeds) {
  var answer = [];

  progresses.reverse(); // for. 스택 사용
  speeds.reverse(); // for. 스택 사용

  while (progresses.length > 0) {
    const day = Math.ceil(
      (100 - progresses[progresses.length - 1]) / speeds[progresses.length - 1]
    ); // 현재 날짜
    const totalProgress = progresses.length; // 이전 작업 수
    progresses.pop();
    speeds.pop();
    answer.push(1);
    for (let i = 0; i < progresses.length; i++) {
      progresses[i] += speeds[i] * day;
    }
    while (progresses.length > 0) {
      if (progresses[progresses.length - 1] < 100) break;
      progresses.pop();
      speeds.pop();
      answer[answer.length - 1]++;
    }
  }

  return answer;
}
```
