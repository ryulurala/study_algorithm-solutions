---
title: "정수 삼각형(1932)"
category: 백준[Class-4]
tags: [C++, JavaScript, 백준]
date: "2021-06-11"
---

## 문제 링크

[정수 삼각형(1932)](https://www.acmicpc.net/problem/1932)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이
void solution(){
    int n;
    cin >> n;

    // input
    vector<vector<int>> dp;
    for(int i=1; i<=n; i++){
        vector<int> sub(i, 0);

        for(int j=0; j<i; j++){
            cin >> sub[j];
        }

        dp.push_back(sub);
    }

    for(int i=1; i<n; i++){
        dp[i][0] += dp[i-1][0];     // 0번째
        dp[i][i] += dp[i-1][i-1];   // 1번째

        for(int j=1; j<=i-1; j++){
            dp[i][j] += max(dp[i-1][j-1], dp[i-1][j]);
        }
    }

    // print
    cout<<*max_element(dp[n-1].begin(), dp[n-1].end())<<endl;
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

const dp = [];
for (let i = 1; i <= n; i++) {
  input[i] = input[i].split(" ");
  dp.push(input[i].map((v) => +v));
}

for (let i = 1; i < n; i++) {
  dp[i][0] += dp[i - 1][0]; // 0 번째
  dp[i][i] += dp[i - 1][i - 1]; // n 번째

  for (let j = 1; j < i; j++) {
    dp[i][j] += Math.max(dp[i - 1][j - 1], dp[i - 1][j]);
  }
}

// print
console.log(Math.max(...dp[n - 1]));
```
