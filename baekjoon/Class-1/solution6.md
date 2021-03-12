---
title: "문자열 반복(2675번)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-12"
---

## 문제 링크

[문자열 반복(2675번)](https://www.acmicpc.net/problem/2675)

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
    for(int i=0; i<n; i++){
        int cnt;
        string str;
        cin >> cnt;
        cin >> str;

        string rst="";
        for(int a=0; a<str.length(); a++){
            for(int b=0; b<cnt; b++){
                rst += str[a];
            }
        }
        cout<<rst<<endl;
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
const input = fs.readFileSync("dev/stdin").toString().split("\n");

// 문제 풀이
const testCount = +input[0];

for (let i = 1; i <= testCount; i++) {
  const testCase = input[i].split(" ");
  const str = testCase[1]
    .split("")
    .map((v) => Array.from({ length: testCase[0] }, () => v).join(""))
    .join("");
  console.log(str);
}
```
