---
title: "이중우선순위큐"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-06"
---

## 문제 링크

[이중우선순위큐](https://programmers.co.kr/learn/courses/30/lessons/42628)

### C++

```cpp
#include <string>
#include <vector>
#include <set>

using namespace std;

vector<int> solution(vector<string> operations) {
    vector<int> answer(2, 0);

    set<int> nums;
    for(string opStr: operations){
        if(opStr[0]=='I') nums.insert(stoi(opStr.substr(2)));
        else if(opStr=="D 1"&&nums.size()>0) nums.erase(--nums.end());
        else if(opStr=="D -1"&&nums.size()>0) nums.erase(nums.begin());
    }
    if(nums.size()>0){
        answer[0]=*(--nums.end());  // 최대
        answer[1]=*nums.begin();    // 최소
    }

    return answer;
}
```

### JavaScript

```js
function solution(operations) {
  var answer = [0, 0];

  const queue = [];
  operations.forEach((v) => {
    if (v[0] === "I") {
      queue.push(parseInt(v.split(" ")[1]));
    } else if (v === "D 1" && queue.length > 0) {
      queue.splice(queue.indexOf(Math.max(...queue)), 1);
    } else if (v === "D -1" && queue.length > 0) {
      queue.splice(queue.indexOf(Math.min(...queue)), 1);
    }
  });

  if (queue.length > 0) {
    answer[0] = Math.max(...queue); // 최대
    answer[1] = Math.min(...queue); // 최소
  }

  return answer;
}
```
