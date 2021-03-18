---
title: "벌집(2292)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-18"
---

## 문제 링크

[벌집(2292)](https://www.acmicpc.net/problem/2292)

## C++

```cpp
#include <iostream>

using namespace std;

// 문제 풀이 함수
void solution(){
    // 1: 1개
    // 2 ~ 7: 6개
    // 8 ~ 19: 12개
    // 20 ~ 37: 18개
    // 38 ~ 61: 24개

    int n;
    cin >> n;

    int limitNum = 1;
    int count=1;
    while(true){
        if(n <= limitNum){
            cout<<count;
            break;
        }

        limitNum += 6*count;
        count++;
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
const n = +input[0];

// 1: 1개
// 2 ~ 7: 6개
// 8 ~ 19: 12개
// 20 ~ 37: 18개
// 38 ~ 61: 24개

let limitNum = 1;
let cnt = 1;
while (true) {
  if (n <= limitNum) {
    console.log(cnt);
    break;
  }

  limitNum += 6 * cnt;
  cnt++;
}
```
