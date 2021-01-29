---
title: "카펫"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-28"
---

## 문제 링크

[카펫](https://programmers.co.kr/learn/courses/30/lessons/42842)

### C++

```cpp
#include <string>
#include <vector>
#include <cmath>

using namespace std;

vector<int> solution(int brown, int yellow) {
    vector<int> answer;

    for(int i=1; i<=sqrt(yellow); i++){
        if(yellow%i!=0) continue;   // 약수가 아니면 skip!

        int width=i+2;      // yellow의 width+2
        int height=(yellow/i)+2;    // yellow의 height+2

        if(brown+yellow!=width*height) continue;

        answer.push_back(max(width, height));   // 큰 수 push
        answer.push_back(min(width, height));   // 작은 수 push
        break;
    }

    return answer;
}
```

### JavaScript

```js
function solution(brown, yellow) {
  var answer = [];

  for (let i = 1; i <= Math.sqrt(yellow); i++) {
    if (yellow % i !== 0) continue; // 약수가 아닐 경우 Skip!

    const width = i + 2; // yellow의 width+2
    const height = yellow / i + 2; // yellow의 height+2

    if (brown + yellow !== width * height) continue;

    answer.push(Math.max(width, height)); // 큰 수가 width
    answer.push(Math.min(width, height)); // 작은 수가 height
  }

  return answer;
}
```
