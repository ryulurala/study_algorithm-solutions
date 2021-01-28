---
title: "타겟 넘버"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-28"
---

## 문제 링크

[타겟 넘버](https://programmers.co.kr/learn/courses/30/lessons/43165)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

void dfsGo(vector<int>& numbers, int& tgt, int& asr, int sum, int level){
    if(level==numbers.size()) {
        if(tgt==sum) asr++;
    }
    else{
        dfsGo(numbers, tgt, asr, sum+numbers[level], level+1);  // +
        dfsGo(numbers, tgt, asr, sum-numbers[level], level+1);  // -
    }
}

int solution(vector<int> numbers, int target) {
    int answer = 0;

    dfsGo(numbers, target, answer, numbers[0], 1);  // +
    dfsGo(numbers, target, answer, -numbers[0], 1); // -

    return answer;
}
```

### JavaScript

```js
function solution(numbers, target) {
  var answer = 0;

  const dfsGo = (sum, level) => {
    if (level === numbers.length) {
      if (sum === target) answer++;
    } else {
      dfsGo(sum + numbers[level], level + 1); // +
      dfsGo(sum - numbers[level], level + 1); // -
    }
  };

  dfsGo(numbers[0], 1); // +
  dfsGo(-numbers[0], 1); // -

  return answer;
}
```
