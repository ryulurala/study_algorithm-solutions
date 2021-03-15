---
title: "개(10172)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-15"
---

## 문제 링크

[개(10172)](https://www.acmicpc.net/problem/10172)

## C++

```cpp
#include <iostream>

using namespace std;

// 문제 풀이 함수
void solution(){
    string str="|\\_/|";
    str += "\n";
    str += "|q p|   /}";
    str += "\n";
    str += "( 0 )\"\"\"\\";
    str += "\n";
    str += "|\"^\"`    |";
    str += "\n";
    str += "||_/=\\\\__|";
    cout<<str<<endl;
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
let str = "|\\_/|";
str += "\n";
str += "|q p|   /}";
str += "\n";
str += '( 0 )"""\\';
str += "\n";
str += '|"^"`    |';
str += "\n";
str += "||_/=\\\\__|";
console.log(str);
```
