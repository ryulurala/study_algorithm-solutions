---
title: "RGB거리(1149)"
category: 백준[Class-4]
tags: [C++, JavaScript, 백준]
date: "2021-06-06"
---

## 문제 링크

[RGB거리(1149)](https://www.acmicpc.net/problem/1149)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

// 문제 풀이
void solution(){
    int n;
    cin >> n;

    vector<vector<int> > dp(n+1, vector<int>(3, 0));
    for(int i=1; i<=n; i++){
        int red, green, blue;
        cin >> red >> green >> blue;

        dp[i][0] = red + min(dp[i-1][1], dp[i-1][2]);
        dp[i][1] = green + min(dp[i-1][0], dp[i-1][2]);
        dp[i][2] = blue + min(dp[i-1][0], dp[i-1][1]);
    }

    cout<<min(dp[n][0], min(dp[n][1], dp[n][2]))<<endl;
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

input[0] = [0, 0, 0];
for (let i = 1; i <= n; i++) {
  input[i] = input[i].split(" ").map((v) => +v);
  input[i][0] += Math.min(input[i - 1][1], input[i - 1][2]);
  input[i][1] += Math.min(input[i - 1][0], input[i - 1][2]);
  input[i][2] += Math.min(input[i - 1][0], input[i - 1][1]);
}

console.log(Math.min(...input[n]));
```
