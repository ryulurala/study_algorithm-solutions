---
title: "최고의 집합"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-16"
---

## 문제 링크

[최고의 집합](https://programmers.co.kr/learn/courses/30/lessons/12938)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

vector<int> solution(int n, int s) {
    vector<int> answer;

    if(s<n){
        answer.push_back(-1);
    }
    else{
        answer.assign(n, s/n);  // n개의 s/n 할당
        int rest=s%n;   // 나머지
        int last=n-1;
        for(int rest=s%n; rest>0; rest--){
            // 나머지를 뒤에서부터 추가
            answer[last--]++;
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(n, s) {
  var answer = [];

  if (s < n) {
    answer.push(-1);
  } else {
    answer = Array.from({ length: n }, () => parseInt(s / n));
    for (let rest = parseInt(s % n); rest > 0; rest--) {
      answer[--n]++;
    }
  }

  return answer;
}
```
