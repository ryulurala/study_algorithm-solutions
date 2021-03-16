---
title: "직사각형에서 탈출(1085)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-16"
---

## 문제 링크

[직사각형에서 탈출(1085)](https://www.acmicpc.net/problem/1085)

## C++

```cpp
#include <iostream>

using namespace std;

// 문제 풀이 함수
void solution(){
    int x, y, w, h;
    cin >> x >> y >> w >> h;

    int minX = min(x, w-x);
    int minY = min(y, h-y);
    cout<<min(minX, minY);
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
const x = +input[0];
const y = +input[1];
const w = +input[2];
const h = +input[3];

const minX = Math.min(x, w - x);
const minY = Math.min(y, h - y);
console.log(Math.min(minX, minY));
```
