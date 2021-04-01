---
title: "피보나치 함수(1003)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-04-01"
---

## 문제 링크

[피보나치 함수(1003)](https://www.acmicpc.net/problem/1003)

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

    // dp(n): [0의 개수, 1의 개수]
    // dp(0): [1, 0] = [1, fibo(0)]
    // dp(1): [0, 1] = [fibo(0), fibo(1)]
    // dp(2): [1, 1] = [fibo(1), fibo(2)]
    // dp(3): [1, 2] = [fibo(2), fibo(3)]
    // dp(4): [2, 3] = [fibo(3), fibo(4)]
    // dp(5): [3, 5] = [fibo(4), fibo(5)]
    vector<int> fibo(41);
    fibo[0]=0;
    fibo[1]=1;
    for(int i=2; i<=40; i++){
        fibo[i] = fibo[i-1]+fibo[i-2];
    }
    // dp(0)을 위해 앞에 1추가
    fibo.insert(fibo.begin(), 1);

    for(int i=0; i<t; i++){
        int n;
        cin >> n;
        cout<<fibo[n]<<" "<<fibo[n+1]<<"\n";
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

// dp(n): [0의 개수, 1의 개수]
// dp(0): [1, 0] = [1, fibo(0)]
// dp(1): [0, 1] = [fibo(0), fibo(1)]
// dp(2): [1, 1] = [fibo(1), fibo(2)]
// dp(3): [1, 2] = [fibo(2), fibo(3)]
// dp(4): [2, 3] = [fibo(3), fibo(4)]
// dp(5): [3, 5] = [fibo(4), fibo(5)]

// 피보나치 수열 구하기
const fibo = Array.from({ length: 41 });
fibo[0] = 0;
fibo[1] = 1;
for (let i = 2; i <= 40; i++) {
  fibo[i] = fibo[i - 1] + fibo[i - 2];
}
fibo.unshift(1); // dp(0)의 0의 개수 추가

const log = [];
for (let i = 1; i <= t; i++) {
  const n = +input[i];
  log.push([fibo[n], fibo[n + 1]]);
}
console.log(log.map((v) => v.join(" ")).join("\n"));
```
