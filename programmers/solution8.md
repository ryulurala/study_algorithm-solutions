---
title: "3진법 뒤집기"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-19"
---

## 문제 링크

[3진법 뒤집기](https://programmers.co.kr/learn/courses/30/lessons/68935)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>
#include <cmath>

using namespace std;

int solution(int n) {
    int answer = 0;

    vector<int> v;

    // 3진법 구하기
    while(true){
        if(n < 1) break;
        v.push_back(n%3);
        n = n/3;
    }

    // 10진법으로 바꾸기
    for(int i=0; i<v.size(); i++){
        answer += v[i] * pow(3, v.size()-i-1);
    }

    return answer;
}
```

### JavaScript

```js
function solution(n) {
  var answer = 0;

  let arr = [];

  // 3진법 바꾸기
  while (true) {
    if (n < 1) break;
    arr.push(Math.floor(n % 3)); // 소수점 버리기
    n /= 3;
  }

  // 10진법 바꾸기
  arr.forEach((value, index, array) => {
    answer += value * Math.pow(3, array.length - index - 1);
  });

  return answer;
}
```
