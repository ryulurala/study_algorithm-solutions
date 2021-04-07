---
title: "계단 오르기(2579)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-04-07"
---

## 문제 링크

[계단 오르기(2579)](https://www.acmicpc.net/problem/2579)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;

    vector<int> stairs(n+1, 0);
    for(int i=1; i<=n; i++){
        cin >> stairs[i];
    }

    if(n==1) cout<<stairs[1];
    else if(n==2) cout<<stairs[1]+stairs[2];
    else if(n==3) cout<<max(stairs[1], stairs[2]) + stairs[3];
    else{
        // dp: 연속 3계단 불가
        // (1). k번을 밟을 경우 + k-2번까지의 최댓값(= dp[k-2])
        // (2). k번을 밟을 경우 + k-1번을 밟을 경우 + k-3번까지의 최댓값(= dp[k-3])
        // k번까지의 최댓값(= dp[k]) = (1), (2)의 최댓값
        vector<int> dp(n+1, 0);
        dp[1] = stairs[1];
        dp[2] = stairs[1]+stairs[2];
        dp[3] = max(stairs[1], stairs[2]) + stairs[3];

        for(int i=4; i<=n; i++){
            dp[i] = max(dp[i-2], dp[i-3]+stairs[i-1])+stairs[i];
        }
        cout<<dp[n];
    }
}

bool exists(const char* fileName){
    FILE* fp;
    if((fp = fopen(fileName, "r"))){
        fclose(fp);
        return true;
    }
    return false;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);

    if(exists("stdin")){
        freopen("stdin", "r", stdin);
        solution();
        fclose(stdin);
    }
    else{
        solution();
    }

    return 0;
}
```

## JavsScript

```js
const fs = require("fs");
const input = fs.readFileSync("dev/stdin").toString().trim().split("\n");

// 문제 풀이
const n = +input[0];
const stairs = input.filter((v, i) => i > 0).map((v) => +v);
stairs.unshift(0); // for. dp.length === stairs.length

if (n === 1) console.log(stairs[1]);
else if (n === 2) console.log(stairs[1] + stairs[2]);
else if (n === 3)
  console.log(Math.max(stairs[1] + stairs[3], stairs[2] + stairs[3]));
else {
  // dp: 연속 3계단 불가
  // (1). k번을 밟을 경우 + k-2번까지의 최댓값(= dp[k-2])
  // (2). k번을 밟을 경우 + k-1번을 밟을 경우 + k-3번까지의 최댓값(= dp[k-3])
  // k번까지의 최댓값(= dp[k]) = (1), (2)의 최댓값
  const dp = Array.from({ length: n + 1 }, () => 0);
  dp[1] = stairs[1];
  dp[2] = stairs[1] + stairs[2];
  dp[3] = Math.max(stairs[1] + stairs[3], stairs[2] + stairs[3]);

  for (let i = 4; i <= n; i++) {
    dp[i] = Math.max(dp[i - 2], dp[i - 3] + stairs[i - 1]) + stairs[i];
  }
  console.log(dp[n]);
}
```
