---
title: "파도반 수열"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-04-20"
---

## 문제 링크

[파도반 수열](https://www.acmicpc.net/problem/9461)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

// 문제 풀이 함수
void solution(){
    int t;
    cin >> t;

    // dp[4] = dp[1]+dp[2]
    // dp[5] = dp[2]+dp[3]
    vector<long long> dp(101, 1);
    for(int i=4; i<=100; i++){
        dp[i] = dp[i-3]+dp[i-2];
    }

    // print
    for(int i=0; i<t; i++){
        int k;
        cin >> k;
        cout<<dp[k]<<"\n";
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
const t = +input[0];
const testCase = input.filter((v, i) => i > 0).map((v) => +v);

// dp[4] = dp[1]+dp[2];
// dp[5] = dp[2]+dp[3];
// dp[6] = dp[3]+dp[4];

const dp = Array.from({ length: 101 }, () => 0);
dp[1] = 1;
dp[2] = 1;
dp[3] = 1;

for (let i = 4; i <= 100; i++) {
  dp[i] = dp[i - 3] + dp[i - 2];
}

const log = [];
testCase.forEach((v) => {
  log.push(dp[v]);
});

// print
console.log(log.join("\n"));
```
