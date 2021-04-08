---
title: "1, 2, 3 더하기(9095)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-04-08"
---

## 문제 링크

[1, 2, 3 더하기(9095)](https://www.acmicpc.net/problem/9095)

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

    vector<int> testCase(t, 0);
    for(int i=0; i<t; i++){
        cin >> testCase[i];
    }

    vector<int> dp(12, 0);
    dp[1] = 1;  // 1
    dp[2] = 2;  // 1+1, 2
    dp[3] = 4;  // 1+1+1, 1+2, 2+1, 3
    dp[4] = 7;  // 1+1+1+1, 1+1+2, 1+2+1, 2+1+1, 1+3, 3+1, 4

    // dp[n] = dp[n-1]+dp[n-2]+dp[n-3]
    for(int i=4; i<=11; i++){
        dp[i] = dp[i-1]+dp[i-2]+dp[i-3];
    }

    for(int num: testCase){
        cout<<dp[num]<<"\n";
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

const dp = Array.from({ length: 12 }, () => 0);
dp[1] = 1; // 1
dp[2] = 2; // 1+1, 2
dp[3] = 4; // 1+1+1, 1+2, 2+1, 3
dp[4] = 7; // 1+1+1+1, 1+1+2, 1+2+1, 2+1+1, 2+2, 1+3, 3+1

// dp[n] = dp[n-1]+dp[n-2]+dp[n-3];
for (let i = 4; i <= 11; i++) {
  dp[i] = dp[i - 1] + dp[i - 2] + dp[i - 3];
}

const log = [];
testCase.forEach((v) => {
  log.push(dp[v]);
});
console.log(log.join("\n"));
```
