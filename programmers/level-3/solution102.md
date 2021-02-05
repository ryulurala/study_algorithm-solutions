---
title: "디스크 컨트롤러"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-05"
---

## 문제 링크

[디스크 컨트롤러](https://programmers.co.kr/learn/courses/30/lessons/42627)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <queue>

using namespace std;

struct cmp{
    bool operator()(vector<int> a, vector<int> b){
        if(a[1]==b[1]) return a[0]>b[0];    // 요청시간 작은 것부터
        else return a[1]>b[1];  // 소요시간 작은 것부터
    }
};

int solution(vector<vector<int>> jobs) {
    int answer = 0;

    priority_queue<vector<int>, vector<vector<int>>, cmp> pq;
    stable_sort(jobs.begin(), jobs.end());  // 요청시간 오름차순
    int i=0;
    int end=0;

    while(!pq.empty()||i<jobs.size()){
        while(i<jobs.size()){
            if(jobs[i][0]>end) break;
            else pq.push(jobs[i++]);    // push: 요청시간<=종료시간
        }
        if(pq.empty()){
            // 큐에 없을 경우 요청 시간 갱신
            end=jobs[i][0];
            continue;
        }
        int req=pq.top()[0];
        int time=pq.top()[1];
        pq.pop();
        end+=time;
        answer+=(end-req);
    }

    return answer/jobs.size();  // 평균
}
```

### JavaScript

```js
function solution(jobs) {
  var answer = 0;

  jobs.sort((a, b) => a[0] - b[0]); // 요청 시간으로 오름차순
  let idx = 0;
  let end = 0;
  const queue = [];

  while (queue.length > 0 || idx < jobs.length) {
    while (idx < jobs.length) {
      if (jobs[idx][0] > end) break;
      queue.push(jobs[idx++]); // push: 요청시간<=종료시간
    }

    if (queue.length === 0) {
      // 큐가 비어있을 경우, 요청시간 갱신
      end = jobs[idx][0];
      continue;
    }

    let minIdx = 0;
    for (let i = 1; i < queue.length; i++) {
      if (queue[i][1] < queue[minIdx][1]) minIdx = i;
    }

    const req = queue[minIdx][0];
    const time = queue[minIdx][1];
    queue.splice(minIdx, 1); // pop
    end += time; // 종료시간 갱신
    answer += end - req;
  }

  return parseInt(answer / jobs.length);
}
```
