---
title: "ATM(11399)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-04-12"
---

## 문제 링크

[ATM(11399)](https://www.acmicpc.net/problem/11399)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;

    vector<int> pNums(n, 0);
    for(int i=0; i<n; i++){
        cin >> pNums[i];
    }

    // 내림차순 정렬
    stable_sort(pNums.rbegin(), pNums.rend());

    int sum=0;
    for(int e: pNums){
        sum += e;
    }

    int result=0;
    for(int e: pNums){
        result += sum;
        sum -= e;
    }
    cout<<result<<"\n";
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
const pNums = input[1].split(" ").map((v) => +v);

pNums.sort((a, b) => a - b);
let sum = pNums.reduce((p, v) => p + v, 0);

let rst = 0;
pNums.reverse().forEach((v) => {
  rst += sum;
  sum -= v;
});

console.log(rst);
```
