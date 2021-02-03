---
title: "풍선 터트리기"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-03"
---

## 문제 링크

[풍선 터트리기](https://programmers.co.kr/learn/courses/30/lessons/68646)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

int solution(vector<int> a) {
    int answer = 2;     // 양 끝

    int leftMin=a.front();
    int rightMin=a.back();

    // 양 끝 제외
    for(int i=1; i<a.size()-1; i++){
        if(a[i]<leftMin){
            leftMin=a[i];
            answer++;
        }
        if(a[a.size()-1-i]<rightMin){
            rightMin=a[a.size()-1-i];
            answer++;
        }
    }
    answer=(leftMin==rightMin)?answer-1:answer;   // 중복됨

    return answer;
}
```

### JavaScript

```js
function solution(a) {
  var answer = 2; // 양 끝

  let leftMin = a[0];
  let rightMin = a[a.length - 1];

  // 양 끝 제외
  for (let i = 1; i < a.length - 1; i++) {
    if (a[i] < leftMin) {
      leftMin = a[i];
      answer++;
    }
    if (a[a.length - 1 - i] < rightMin) {
      rightMin = a[a.length - 1 - i];
      answer++;
    }
  }

  answer = leftMin === rightMin ? answer - 1 : answer; // 중복제거

  return answer;
}
```
