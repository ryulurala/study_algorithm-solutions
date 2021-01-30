---
title: "피보나치 수"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-31"
---

## 문제 링크

[피보나치 수](https://programmers.co.kr/learn/courses/30/lessons/12945)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

int solution(int n) {
    int answer = 0;

    vector<int> fibo(100001);
    fibo[0]=0;
    fibo[1]=1;
    for(int i=2; i<=n; i++){
        fibo[i]=fibo[i-1]+fibo[i-2];
        fibo[i]%=1234567;
    }

    answer=fibo[n];

    return answer;
}
```

### JavaScript

```js
function solution(n) {
  var answer = 0;

  const fibo = Array.from({ length: 10001 }, () => 0);
  fibo[0] = 0;
  fibo[1] = 1;
  for (let i = 2; i <= n; i++) {
    fibo[i] = fibo[i - 1] + fibo[i - 2];
    fibo[i] %= 1234567;
  }

  answer = fibo[n];

  return answer;
}
```
