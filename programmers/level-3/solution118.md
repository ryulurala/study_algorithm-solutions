---
title: "거스름돈"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-13"
---

## 문제 링크

[거스름돈](https://programmers.co.kr/learn/courses/30/lessons/12907)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(int n, vector<int> money) {
    int answer = 0;

    stable_sort(money.begin(), money.end());    // 작은 단위부터

    vector<int> dp(n+1, 0);     // 경우의 수
    dp[0]=1;    // init
    for(int current: money){
        for(int i=current; i<=n; i++){
            // 해당 화폐(current)가 사용될 때부터
            dp[i]+=dp[i-current];
            dp[i]%=1000000007;  // 미리 나누기
        }
    }
    answer=dp[n];

    return answer;
}
```

### JavaScript

```js
function solution(n, money) {
  var answer = 0;

  money.sort((a, b) => a - b); // 작은 단위부터
  const dp = Array.from({ length: n + 1 }, () => 0);
  dp[0] = 1; // init

  money.forEach((value) => {
    for (let i = value; i <= n; i++) {
      // value~n 까지 갱신
      dp[i] += dp[i - value]; // [i-value] 경우의 수 추가
      dp[i] %= 1000000007; // 미리 나누기
    }
  });
  answer = dp[n];

  return answer;
}
```
