---
title: "음양 더하기"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-04-17"
---

## 문제 링크

[음양 더하기](https://programmers.co.kr/learn/courses/30/lessons/76501)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

int solution(vector<int> absolutes, vector<bool> signs) {
    int answer = 0;

    for(int i=0; i<signs.size(); i++){
        if(signs[i]) answer += absolutes[i];
        else answer -= absolutes[i];
    }

    return answer;
}
```

### JavaScript

```js
function solution(absolutes, signs) {
  var answer = 0;

  signs.forEach((v, i) => {
    if (v) answer += absolutes[i];
    else answer -= absolutes[i];
  });

  return answer;
}
```
