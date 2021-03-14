---
title: "별 찍기 - 2(2439)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-14"
---

## 문제 링크

[별 찍기 - 2(2439)](https://www.acmicpc.net/problem/2439)

## C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;
    for(int i=1; i<=n; i++){
        string str1(n-i, ' ');
        string str2(i, '*');
        cout << str1+str2 << endl;
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
const input = fs.readFileSync("dev/stdin").toString().trim().split(" ");

// 문제 풀이
const n = input[0];

for (let i = 1; i <= n; i++) {
  console.log(" ".repeat(n - i) + "*".repeat(i));
}
```
