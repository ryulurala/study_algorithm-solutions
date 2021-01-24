---
title: "나누어 떨어지는 숫자 배열"
excerpt: "프로그래머스 풀이"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
toc: true
toc_sticky: true
---

## 문제 링크

[나누어 떨어지는 숫자 배열](https://programmers.co.kr/learn/courses/30/lessons/12910)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(vector<int> arr, int divisor) {
    vector<int> answer;

    for(auto e: arr){
        if(e%divisor==0){
            // 나누어 떨어질 경우 push
            answer.push_back(e);
        }
    }

    if(answer.empty())
        answer.push_back(-1);   // -1 push
    else
        sort(answer.begin(), answer.end());     // 오름차순 정렬

    return answer;
}
```

### JavaScript

```js
function solution(arr, divisor) {
  var answer = [];

  arr.forEach((value, index, array) => {
    if (value % divisor === 0) {
      // 나누어 떨어질 경우 push
      answer.push(value);
    }
  });

  if (answer.length != 0) {
    // 오름차순 정렬
    answer.sort((a, b) => {
      return a < b ? -1 : a === 0 ? 0 : 1;
    });
  } else {
    answer.push(-1);
  }

  return answer;
}
```
