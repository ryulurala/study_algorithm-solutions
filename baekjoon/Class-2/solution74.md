---
title: "소수 구하기(1929)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-30"
---

## 문제 링크

[소수 구하기(1929)](https://www.acmicpc.net/problem/1929)

## C++

```cpp
#include <iostream>
#include <vector>
#include <cmath>

using namespace std;

// 문제 풀이 함수
void solution(){
    int m, n;
    cin >> m >> n;

    vector<bool> primeNums(n+1, true);
    primeNums[0] = false;   // 0은 소수 [X]
    primeNums[1] = false;   // 1은 소수 [X]

    for(int i=2; i<=sqrt(n); i++){
        if(primeNums[i] == false) continue;
        for(int j=i+i; j<=n; j+=i){
            // 소수의 배수는 소수가 아니다.
            primeNums[j] = false;
        }
    }

    string log = "";
    for(int i=m; i<=n; i++){
        if(primeNums[i] == true)
            log += to_string(i) + "\n";
    }
    cout<<log;
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
const input = fs.readFileSync("dev/stdin").toString().trim().split(" ");

// 문제 풀이
const m = +input[0];
const n = +input[1];

// 일단 모두 소수
const primeNums = Array.from({ length: n + 1 }, () => true);
primeNums[0] = false; // 0은 소수 [X]
primeNums[1] = false; // 1은 소수 [X]

for (let i = 2; i <= parseInt(Math.sqrt(n)); i++) {
  if (primeNums[i] === false) continue;
  for (let j = i + i; j <= n; j += i) {
    // 소수의 배수는 모두 소수 [X]
    primeNums[j] = false;
  }
}

// print
const log = [];
for (let i = m; i <= n; i++) {
  if (primeNums[i]) log.push(i);
}
console.log(log.join("\n"));
```
