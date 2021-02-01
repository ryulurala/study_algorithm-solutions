---
title: "N개의 최소공배수"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-01"
---

## 문제 링크

[N개의 최소공배수](https://programmers.co.kr/learn/courses/30/lessons/12953)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

int gcd(int a, int b){  // 최대공약수
    if(a%b==0) return b;
    else return gcd(b, a%b);
}

int lcm(int a, int b){  // 최소공배수
    return a*b/gcd(a, b);
}

int solution(vector<int> arr) {
    int answer = 1;

    for(int num: arr){
        answer=lcm(answer, num);
    }

    return answer;
}
```

### JavaScript

```js
function solution(arr) {
  var answer = 1;

  // 최대공약수
  const gcd = (a, b) => {
    if (a % b === 0) return b;
    else return gcd(b, a % b);
  };

  // 최소공배수
  const lcm = (a, b) => (a * b) / gcd(a, b);

  arr.forEach((v) => {
    answer = lcm(answer, v);
  });

  return answer;
}
```
