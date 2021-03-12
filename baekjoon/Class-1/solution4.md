---
title: "별 찍기 - 1(2438번)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-12"
---

## 문제 링크

[별 찍기 - 1(2438번)](https://www.acmicpc.net/problem/2438)

## C++

```cpp
#include <iostream>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n=0;
    cin >> n;
    for(int i=1; i<=n; i++){
        for(int j=0; j<i; j++){
            printf("*");
        }
        printf("\n");
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
const input = fs.readFileSync("dev/stdin").toString().split(" ");

// 문제 풀이
const n = parseInt(input[0]);

for (let i = 1; i <= n; i++) {
  console.log(Array.from({ length: i }, () => "*").join(""));
}
```
