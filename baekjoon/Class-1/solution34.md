---
title: "숫자의 합(11720)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-16"
---

## 문제 링크

[숫자의 합(11720)](https://www.acmicpc.net/problem/11720)

## C++

```cpp
#include <iostream>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    string str;
    cin >> n >> str;
    int sum=0;
    for(char ch: str){
        int num = ch - '0';
        sum += num;
    }
    cout<<sum;
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
const sum = input[1].split("").reduce((p, v) => p + +v, 0);
console.log(sum);
```
