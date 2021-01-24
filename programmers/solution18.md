---
title: "소수 찾기"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[소수 찾기](https://programmers.co.kr/learn/courses/30/lessons/12921)

### C++

```cpp
#include <string>
#include <vector>
#include <cmath>

using namespace std;

int solution(int n) {
    int answer = 0;
    vector<bool> check(n+1, true);  // 인덱스 n까지 처음에는 모두 소수

    for(int i=2; i<=sqrt(n); i++){
        if(!check[i]) continue;     // 이미 소수가 아님
        for(int j=i+i; j<=n; j+=i){
            // 해당 배수는 모두 소수가 아님
            check[j] = false;
        }
    }

    for(int i=0; i<check.size(); i++){
        if(check[i]) answer++;      // 소수들
    }

    return answer-2;    // 0과 1은 제외
}
```

### JavaScript

```js
function solution(n) {
  var answer = 0;

  let arr = Array.from({ length: n + 1 }, (value, index) => {
    return 1; // 일단 모두 소수
  });

  for (let i = 2; i <= Math.sqrt(n); i++) {
    if (arr[i] === 0) continue; // 이미 소수가 아님
    for (let j = i + i; j <= n; j += i) {
      // 소수의 배수는 모두 소수가 아님
      arr[j] = 0;
    }
  }
  arr.forEach((value, index, array) => {
    if (value === 1) answer++;
  });

  return answer - 2; // 0과 1은 제외
}
```
