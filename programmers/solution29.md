---
title: "제일 작은 수 제거하기"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[제일 작은 수 제거하기](https://programmers.co.kr/learn/courses/30/lessons/12935)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(vector<int> arr) {
    vector<int> answer;

    if(arr.size()==1){
        answer.push_back(-1);
    }
    else{
        auto iter = min_element(arr.begin(), arr.end());
        arr.erase(iter);
        swap(answer, arr);
    }

    return answer;
}
```

### JavaScript

```js
function solution(arr) {
  var answer = [];

  if (arr.length === 1) {
    answer.push(-1);
  } else {
    let min = Math.min(...arr);
    arr.splice(arr.indexOf(min), 1);
    answer = arr.slice();
  }

  return answer;
}
```
