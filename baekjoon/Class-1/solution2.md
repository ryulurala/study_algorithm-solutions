---
title: "두 수 비교하기(1330번)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: ""
---

## 문제 링크

[두 수 비교하기(1330번)](https://www.acmicpc.net/problem/1330)

## C++

```cpp
#include <iostream>

using namespace std;

// 문제 풀이
void solution(){
    // cin 조절
    int a=0, b=0;
    cin >> a >> b;

    if(a > b)
        cout << ">";
    else if(a < b)
        cout << "<";
    else if(a == b)
        cout << "==";
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
if (+input[0] > +input[1]) console.log(">");
else if (+input[0] < +input[1]) console.log("<");
else console.log("==");
```
