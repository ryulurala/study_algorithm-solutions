---
title: "수 정렬하기(2750)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-17"
---

## 문제 링크

[수 정렬하기(2750)](https://www.acmicpc.net/problem/2750)

## C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, a;
    cin >> n;

    vector<int> vec;
    while(cin >> a)
        vec.push_back(a);

    stable_sort(vec.begin(), vec.end());

    for(int e: vec){
        cout<<e<<endl;
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
const input = fs.readFileSync("dev/stdin").toString().trim().split("\n");

// 문제 풀이
const n = +input[0];

const arr = [];
for (let i = 1; i <= n; i++) {
  arr.push(+input[i]);
}
arr.sort((a, b) => a - b);

console.log(arr.join("\n"));
```
