---
title: "행렬의 덧셈"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[행렬의 덧셈](https://programmers.co.kr/learn/courses/30/lessons/12950)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

vector<vector<int>> solution(vector<vector<int>> arr1, vector<vector<int>> arr2) {
    vector<vector<int>> answer;

    for(int i=0; i<arr1.size(); i++){
        vector<int> sum;
        for(int j=0; j<arr1[i].size(); j++){
            sum.push_back(arr1[i][j] + arr2[i][j]);
        }
        answer.push_back(sum);
    }

    return answer;
}
```

### JavaScript

```js
function solution(arr1, arr2) {
  var answer = [];

  for (let i = 0; i < arr1.length; i++) {
    const arr = [];
    for (let j = 0; j < arr1[i].length; j++) {
      arr.push(arr1[i][j] + arr2[i][j]);
    }
    answer.push(arr);
  }

  return answer;
}
```
