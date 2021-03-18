---
title: "달팽이는 올라가고 싶다(2869)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-18"
---

## 문제 링크

[달팽이는 올라가고 싶다(2869)](https://www.acmicpc.net/problem/2869)

## C++

```cpp
#include <iostream>
#include <vector>
#include <cmath>

using namespace std;

// 문제 풀이 함수
void solution(){
    int a, b, v;
    cin >> a >> b >> v;

    if(v>a){
        cout<<(int)ceil((double)(v-a)/(a-b))+1<<endl;
    }
    else{
        // 하루만에 올라감
        cout<<1<<endl;
    }
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
const a = +input[0];
const b = +input[1];
const v = +input[2];

if (v > a) {
  console.log(Math.ceil((v - a) / (a - b)) + 1);
} else {
  console.log(1);
}
```
