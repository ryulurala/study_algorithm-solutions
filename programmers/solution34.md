---
title: "평균 구하기"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[평균 구하기](https://programmers.co.kr/learn/courses/30/lessons/12944)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

double solution(vector<int> arr) {
    double answer = 0;

    for(auto e: arr){
        answer += e;
    }
    answer /= arr.size();

    return answer;
}
```

### JavaScript

```js
function solution(arr) {
  var answer = 0;

  arr.forEach((value) => {
    answer += value;
  });
  answer /= arr.length;

  return answer;
}
```
