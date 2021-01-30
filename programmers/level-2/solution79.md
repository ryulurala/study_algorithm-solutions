---
title: "행렬의 곱셈"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-31"
---

## 문제 링크

[행렬의 곱셈](https://programmers.co.kr/learn/courses/30/lessons/12949)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

vector<vector<int>> solution(vector<vector<int>> arr1, vector<vector<int>> arr2) {
    vector<vector<int>> answer;

    for(int i=0; i<arr1.size(); i++){
        vector<int> v;
        for(int j=0; j<arr2[0].size(); j++){
            int sum=0;
            for(int k=0; k<arr2.size(); k++){
                sum+=arr1[i][k]*arr2[k][j];
            }
            v.push_back(sum);
        }
        answer.push_back(v);
    }

    return answer;
}
```

### JavaScript

```js
function solution(arr1, arr2) {
  var answer = [];

  for (let i = 0; i < arr1.length; i++) {
    const rst = [];
    for (let j = 0; j < arr2[0].length; j++) {
      let sum = 0;
      for (let k = 0; k < arr2.length; k++) {
        sum += arr1[i][k] * arr2[k][j];
      }
      rst.push(sum);
    }
    answer.push(rst);
  }

  return answer;
}
```
