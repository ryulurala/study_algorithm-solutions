---
title: "Four Squares(17626)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-03-31"
---

## 문제 링크

[Four Squares(17626)](https://www.acmicpc.net/problem/17626)

## C++

```cpp
#include <iostream>
#include <vector>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;

    vector<int> dp(n+1);
    dp[0] = 0;
    dp[1] = 1;
    for(int i=1; i<=n; i++){
        // i = 1 + i-1까지 최소갯수
        dp[i] = dp[1] + dp[i-1];
        for(int j=2; j*j<=i; j++){
            // i의 최소갯수 = min(i의 최소 갯수, 완전제곱수 + i-완전제곱수)
            // 완전 제곱수일 때는 1개로 구성됨
            dp[i] = min(dp[i], 1+dp[i-j*j]);
        }
    }
    cout<<dp[n]<<"\n";
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

const dp = Array.from({ length: n + 1 }, () => 0);
dp[0] = 0;
dp[1] = 1;
for (let i = 1; i <= n; i++) {
  // i = 1 + i-1까지 최소갯수
  dp[i] = dp[1] + dp[i - 1];

  for (let j = 2; j * j <= i; j++) {
    // i의 최소갯수 = min(i의 최소 갯수, 완전제곱수 + i-완전제곱수)
    // 완전 제곱수일 때는 1개로 구성됨
    dp[i] = Math.min(dp[i], 1 + dp[i - j * j]);
  }
}
console.log(dp[n]);
```
