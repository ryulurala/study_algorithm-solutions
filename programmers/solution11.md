---
title: "같은 숫자는 싫어"
excerpt: "프로그래머스 풀이"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
toc: true
toc_sticky: true
---

## 문제 링크

[같은 숫자는 싫어](https://programmers.co.kr/learn/courses/30/lessons/12906)

### C++

```cpp
#include <vector>
#include <iostream>

using namespace std;

vector<int> solution(vector<int> arr)
{
    vector<int> answer;

    for(auto e: arr){
        if(answer.empty() || answer.back() != e){
            // 비어있거나 마지막 수가 다를 경우 push
            answer.push_back(e);
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(arr) {
  var answer = [];

  arr.forEach((value, index, array) => {
    if (index == 0 || answer[answer.length - 1] != value) {
      // 비어있거나 answer 마지막 수가 다를 경우 push
      answer.push(value);
    }
  });

  return answer;
}
```
