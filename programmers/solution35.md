---
title: "하샤드 수"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[하샤드 수](https://programmers.co.kr/learn/courses/30/lessons/12947)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

bool solution(int x) {
    bool answer = true;

    int sum = 0;
    string str = to_string(x);
    for(char c: str){
        sum += (c - '0');
    }
    answer = (x%sum==0) ? true : false;

    return answer;
}
```

### JavaScript

```js
function solution(x) {
  var answer = true;

  let sum = 0;
  x.toString()
    .split("")
    .forEach((value) => {
      sum += value - "0";
    });
  answer = x % sum === 0 ? true : false;

  return answer;
}
```
