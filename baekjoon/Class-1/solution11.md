---
title: "사칙연산(10869)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-13"
---

## 문제 링크

[사칙연산(10869)](https://www.acmicpc.net/problem/10869)

## C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    int a, b;
    cin >> a >> b;
    cout<<a+b<<endl;
    cout<<a-b<<endl;
    cout<<a*b<<endl;
    cout<<a/b<<endl;
    cout<<a%b<<endl;
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
const a = +input[0];
const b = +input[1];

console.log(
  `${a + b}
${a - b}
${a * b}
${parseInt(a / b)}
${a % b}`
);
```
