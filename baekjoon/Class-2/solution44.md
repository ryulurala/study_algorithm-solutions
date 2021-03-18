---
title: "부녀회장이 될테야(2775)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-18"
---

## 문제 링크

[부녀회장이 될테야(2775)](https://www.acmicpc.net/problem/2775)

## C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    int t, k, n;
    cin >> t;

    // parsing
    vector<int> Ks;
    vector<int> Ns;
    while(cin >> k >> n){
        Ks.push_back(k);
        Ns.push_back(n);
    }

    // 최대 층, 최대 호 수
    int maxK = *max_element(Ks.begin(), Ks.end());
    int maxN = *max_element(Ns.begin(), Ns.end());

    // Look up table
    vector<vector<int> > LUT(maxK+1, vector<int>(maxN+1, 0));

    // Init LUT: 0층
    for(int i=1; i<=maxN; i++){
        LUT[0][i]=i+LUT[0][i-1];
    }

    // DP
    for(int i=1; i<=maxK; i++){
        for(int j=1; j<=maxN; j++){
            LUT[i][j]=LUT[i-1][j]+LUT[i][j-1];
        }
    }

    // result
    for(int i=0; i<t; i++){
        k = Ks[i];
        n = Ns[i];

        // K층 N호 거주민 수 = K층 N호까지의 거주민 총 합 - K층 N-1호까지의 거주민 총 합
        cout<<LUT[k][n]-LUT[k][n-1]<<endl;
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
// split 조절
const input = fs.readFileSync("dev/stdin").toString().trim().split("\n");

// 문제 풀이
const t = +input[0];

// max 층, 호 구하기: for. Look up table
const floors = input.filter((v, i) => i !== 0).filter((v, i) => +i % 2 === 0);
const maxFloor = Math.max(...floors);
const maxHo = 14;

// lut[k][n]: k층에 n호
const lut = Array.from({ length: maxFloor + 1 }, () =>
  Array.from({ length: maxHo + 1 }, () => 0)
);

// init look up table
for (let i = 1; i <= maxHo; i++) {
  lut[0][i] = lut[0][i - 1] + i;
}

// DP
for (let i = 1; i <= maxFloor; i++) {
  for (let j = 1; j <= maxHo; j++) {
    lut[i][j] = lut[i - 1][j] + lut[i][j - 1];
  }
}

// parsing
for (let i = 1; i <= t * 2; i += 2) {
  const k = +input[i];
  const n = +input[i + 1];

  // k층 n호 거주민 = k층의 n호까지의 거주민 수들의 합 - k층의 n-1호까지의 거주민 수들의 합
  console.log(lut[k][n] - lut[k][n - 1]);
}
```
