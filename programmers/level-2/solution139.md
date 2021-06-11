---
title: "2개 이하로 다른 비트"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-06-11"
---

## 문제 링크

[2개 이하로 다른 비트](https://programmers.co.kr/learn/courses/30/lessons/77885)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

vector<long long> solution(vector<long long> numbers) {
    vector<long long> answer;

    for(long long x: numbers){
        // 짝수 or 홀수
        if(x%2==0) {
            answer.push_back(x+1);
        }
        else{
            long long lastZero = (x+1)&(-x);    // 마지막 0 bit 자리
            x |= lastZero;  // 마지막 0을 1로
            x &= ~(lastZero>>1);    // 그 다음 bit를 0으로

            answer.push_back(x);
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(numbers) {
  var answer = [];

  numbers.forEach((x) => {
    x = BigInt(x);

    // x가 짝수 or 홀수
    if (x % 2n === 0n) {
      answer.push(x + 1n); // 마지막 bit만 1로 바꿈
    } else {
      const lastZeroPos = (x + 1n) & -x; // 마지막 0 bit 위치
      x |= lastZeroPos; // 마지막 0 bit 위치: 0 -> 1
      x &= ~(lastZeroPos >> 1n); // 그 다음 위치: 1 -> 0

      answer.push(x);
    }
  });

  return answer;
}
```
