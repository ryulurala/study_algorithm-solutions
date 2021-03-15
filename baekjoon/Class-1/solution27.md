---
title: "나머지(3052)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-15"
---

## 문제 링크

[나머지(3052)](https://www.acmicpc.net/problem/3052)

## C++

```cpp
#include <iostream>
#include <algorithm>
#include <map>

using namespace std;

// 문제 풀이 함수
void solution(){
    map<int, int> m;
    int a;
    while(cin >> a){
        m[a%42]++;
    }
    cout<<m.size()<<endl;
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
const nums = input.map((v) => +v);
const s = new Set();
nums.forEach((v) => s.add(v % 42));
console.log(s.size);
```
