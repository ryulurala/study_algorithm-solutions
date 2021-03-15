---
title: "알람 시계(2884)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-15"
---

## 문제 링크

[알람 시계(2884)](https://www.acmicpc.net/problem/2884)

## C++

```cpp
#include <iostream>
#include <map>

using namespace std;

// 문제 풀이 함수
void solution(){
    int h, m;
    cin >> h >> m;
    h = (m-45>=0) ? h : (h-1<0) ? 23 : h-1;
    m = (m-45>=0) ? m-45 : m+15;
    cout<<h<<" "<<m<<endl;
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
let h = +input[0];
let m = +input[1];
h = m - 45 >= 0 ? h : h - 1 < 0 ? 23 : h - 1;
m = m - 45 >= 0 ? m - 45 : m + 15;

console.log(`${h} ${m}`);
```
