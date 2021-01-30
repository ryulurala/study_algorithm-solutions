---
title: "폰켓몬"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-30"
---

## 문제 링크

[폰켓몬](https://programmers.co.kr/learn/courses/30/lessons/1845)

### C++

```cpp
#include <vector>
#include <set>

using namespace std;

int solution(vector<int> nums) {
    int answer = 0;

    set<int> bag;   // 중복 제거
    for(int num: nums) bag.insert(num);

    answer = (bag.size()>nums.size()/2) ? nums.size()/2 : bag.size();

    return answer;
}
```

### JavaScript

```js
function solution(nums) {
  var answer = 0;

  const bag = new Set(nums);
  answer =
    bag.size > parseInt(nums.length / 2) ? parseInt(nums.length / 2) : bag.size;

  return answer;
}
```
