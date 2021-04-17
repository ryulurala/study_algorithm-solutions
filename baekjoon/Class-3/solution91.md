---
title: "2×n 타일링(11726)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-04-17"
---

## 문제 링크

[2×n 타일링(11726)](https://www.acmicpc.net/problem/11726)

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

    if(n==1) cout<<1<<"\n";
    else{
        // 2x1: 1
        // 2x2: 2
        // 2x3: 3
        // 2x4: 5
        // 2x9: 55
        vector<int> dp(n+1, 0);
        dp[1]=1;
        dp[2]=2;
        for(int i=3; i<=n; i++){
            dp[i] = dp[i-1]+dp[i-2];
            dp[i] %= 10007;
        }
        cout<<dp[n]<<"\n";
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

if (n === 1) {
  console.log(1);
} else {
  // 2x1: 1
  // 2x2: 2
  // 2x3: 3
  // 2x4: 5
  // 2x9: 55
  const dp = Array.from({ length: n + 1 }, () => 0);
  dp[1] = 1;
  dp[2] = 2;
  for (let i = 3; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
    dp[i] %= 10007;
  }

  // print
  console.log(dp[n]);
}
```
