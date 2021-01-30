---
title: "숫자의 표현"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-31"
---

## 문제 링크

[숫자의 표현](https://programmers.co.kr/learn/courses/30/lessons/12924)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

int solution(int n) {
    int answer = 1;     // 자기 자신

    int limit=(n%2)?(n+1)/2:n/2;
    int sum=0;
    int sub=1;      // 1부터 빼기
    for(int i=1; i<=limit; i++){
        sum += i;
        if(sum>=n){
            while(sum>n) sum-=sub++;
            if(sum==n) answer++;
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(n) {
  var answer = 1; // 자기 자신

  const limit = n % 2 ? (n + 1) / 2 : n / 2; // 홀수일 경우 (n+1)/2

  let sum = 0;
  let shift = 1; // 1부터 빼기
  for (let i = 1; i <= limit; i++) {
    sum += i;
    if (sum >= n) {
      while (sum > n) sum -= shift++;
      if (sum === n) answer++;
    }
  }

  return answer;
}
```
