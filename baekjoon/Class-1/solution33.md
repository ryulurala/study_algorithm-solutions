---
title: "아스키 코드(11654)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-16"
---

## 문제 링크

[아스키 코드(11654)](https://www.acmicpc.net/problem/11654)

## C++

```cpp
#include <iostream>

using namespace std;

// 문제 풀이 함수
void solution(){
    char ch;
    cin >> ch;
    printf("%d", ch);
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
const w = input[0];
console.log(w.charCodeAt());
```
