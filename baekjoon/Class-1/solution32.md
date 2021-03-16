---
title: "X보다 작은 수(10871)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-16"
---

## 문제 링크

[X보다 작은 수(10871)](https://www.acmicpc.net/problem/10871)

## C++

```cpp
#include <iostream>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, x;
    cin >> n >> x;
    string str="";
    for(int i=0; i<n; i++){
        int a;
        cin >> a;
        if(x <= a) continue;
        str += to_string(a) + " ";
    }
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
const n = +input[0].split(" ")[0];
const x = +input[0].split(" ")[1];
const nums = input[1].split(" ").map((v) => +v);

console.log(nums.filter((v) => x > v).join(" "));
```
