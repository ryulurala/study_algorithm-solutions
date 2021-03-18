---
title: "분해합(2231)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-18"
---

## 문제 링크

[분해합(2231)](https://www.acmicpc.net/problem/2231)

## C++

```cpp
#include <iostream>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;

    // 자릿수 * 9가 최소 시작
    int delta = 9*to_string(n).length();

    bool hasInitNum = false;
    for(int i=n-delta; i<n; i++){
        // 분해합
        int sum = i;
        string str=to_string(i);
        for(char ch: str){
            sum += ch - '0';
        }

        if(sum == n){
            cout<<i;
            hasInitNum = true;
            break;
        }
    }

    if(!hasInitNum) cout<<0;
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

// n - 자릿 수 * 9가 최소 시작
const delta = 9 * n.toString().length;

let hasInitNum = false;
for (let i = n - delta; i < n; i++) {
  // 분해합
  const sum =
    i +
    i
      .toString()
      .split("")
      .reduce((p, v) => p + +v, 0);

  if (sum === n) {
    console.log(i);
    hasInitNum = true;
    break;
  }
}
if (!hasInitNum) console.log(0);
```
