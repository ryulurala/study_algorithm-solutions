---
title: "검증수(2475)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-14"
---

## 문제 링크

[검증수(2475)](https://www.acmicpc.net/problem/2475)

## C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    int sum=0;
    int a;
    while(cin >> a){
        sum += (a*a);
    }
    cout<<sum%10<<endl;
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
const sum = input.reduce((p, v) => p + v * v, 0);
console.log(sum % 10);
```
