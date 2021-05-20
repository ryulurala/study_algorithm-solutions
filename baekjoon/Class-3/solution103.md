---
title: "동전 0(11047)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-05-20"
---

## 문제 링크

[동전 0(11047)](https://www.acmicpc.net/problem/11047)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

void solution(){
    int n, k;
    cin >> n >> k;

    vector<int> coins;
    for(int i=0; i<n; i++){
        int coin;
        cin >> coin;

        coins.push_back(coin);
    }

    // 가치가 큰 동전부터 진행(greedy)
    int total = k;
    int count = 0;
    for(int i=coins.size()-1; i>=0; i--){
        int coin = coins[i];
        if(total >= coin){
            count += total/coin;
            total %= coin;
        }
    }

    cout<<count<<"\n";
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
input[0] = input[0].split(" ");
const n = +input[0][0];
const k = +input[0][1];

// 가치가 큰 동전부터 나오도록 뒤집어줌
const coins = input
  .filter((v, i) => i > 0)
  .map((v) => +v)
  .reverse();

// greedy
let count = 0;
let total = k;
for (const coin of coins) {
  if (coin <= total) {
    count += Math.floor(total / coin);
    total %= coin;
  }
}

console.log(count);
```
