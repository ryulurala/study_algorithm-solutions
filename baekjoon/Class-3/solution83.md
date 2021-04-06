---
title: "팩토리얼 0의 개수(1676)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-04-06"
---

## 문제 링크

[팩토리얼 0의 개수(1676)](https://www.acmicpc.net/problem/1676)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <queue>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;

    int count=0;
    while(n>0){
        n /= 5;
        count += n;
    }
    cout<<count;
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
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);

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
const input = fs.readFileSync("dev/stdin").toString().trim().split("\n");

// 문제 풀이
let n = +input[0];

// 소인수 5의 개수
let cnt = 0;
while (n > 0) {
  n = parseInt(n / 5);
  cnt += n;
}
console.log(cnt);
```
