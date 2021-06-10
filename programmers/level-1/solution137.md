---
title: "약수의 개수와 덧셈"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-06-11"
---

## 문제 링크

[약수의 개수와 덧셈](https://programmers.co.kr/learn/courses/30/lessons/77884)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

int solution(int left, int right) {
    int answer = 0;

    // 1 ~ 1000까지 약수의 개수 구하기
    vector<int> divisor(1001, 0);
    for(int i=1; i<=1000; i++){
        for(int j=1; j<=1000/i; j++){
            divisor[i*j]++;
        }
    }

    for(int i=left; i<=right; i++){
        if(divisor[i]%2==0)
            answer += i;    // 짝수
        else
            answer -= i;    // 홀수
    }

    return answer;
}
```

### JavaScript

```js
function solution(left, right) {
  var answer = 0;

  // 1 ~ 1000까지 약수의 개수 구하기
  const divisor = Array(1001).fill(0);
  for (let i = 1; i <= 1000; i++) {
    for (let j = 1; j <= Math.floor(1000 / i); j++) {
      divisor[i * j]++;
    }
  }

  for (let i = left; i <= right; i++) {
    if (divisor[i] % 2 === 0) answer += i;
    // 짝수
    else answer -= i; // 홀수
  }

  return answer;
}
```
