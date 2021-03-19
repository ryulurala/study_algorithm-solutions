---
title: "영화감독 숌(1436)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-19"
---

## 문제 링크

[영화감독 숌(1436)](https://www.acmicpc.net/problem/1436)

## C++

```cpp
const fs = require("fs");
// split 조절
const input = fs.readFileSync("dev/stdin").toString().trim().split("\n");

// 문제 풀이
const n= +input[0];

let cnt=0;
let num=666;
while(true){
    if(num.toString().includes("666")){
        cnt++;
        if(cnt===n) break;
    }
    num++;
}
console.log(num);
```

## JavsScript

```js
#include <iostream>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;

    int cnt=1;
    int num=666;
    while(true){
        if(to_string(num).find("666") != string::npos){
            if(cnt==n) break;
            cnt++;
        }
        num++;
    }
    cout<<num;
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
