---
title: "최댓값과 최솟값"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-31"
---

## 문제 링크

[최댓값과 최솟값](https://programmers.co.kr/learn/courses/30/lessons/12939)

### C++

```cpp
#include <string>
#include <vector>
#include <sstream>
#include <algorithm>

using namespace std;

string solution(string s) {
    string answer = "";

    stringstream ss(s);
    vector<int> nums;
    int num;
    while(ss>>num) nums.push_back(num);

    answer=to_string(*min_element(nums.begin(), nums.end()))
        + " " + to_string(*max_element(nums.begin(), nums.end()));

    return answer;
}
```

### JavaScript

```js
function solution(s) {
  var answer = "";

  const arr = s.split(" ");
  answer += Math.min(...arr) + " " + Math.max(...arr);

  return answer;
}
```
