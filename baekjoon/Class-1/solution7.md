---
title: "구구단(2739)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-13"
---

## 문제 링크

[구구단(2739)](https://www.acmicpc.net/problem/2739)

## C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;
    for(int i=1; i<=9; i++){
        printf("%d * %d = %d\n", n, i, n*i);
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
const input = fs.readFileSync("dev/stdin").toString().split(" ");

// 문제 풀이
const n = +input[0];

for (let i = 1; i <= 9; i++) {
  console.log(`${n} * ${i} = ${n * i}`);
}
```
