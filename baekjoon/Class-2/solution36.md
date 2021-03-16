---
title: "직각삼각형(4153)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-16"
---

## 문제 링크

[직각삼각형(4153)](https://www.acmicpc.net/problem/4153)

## C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    int a, b, c;
    while(cin>>a>>b>>c){
        if(a==0 && b==0 && c==0) break;
        vector<int> vec(3);
        vec[0]=a;
        vec[1]=b;
        vec[2]=c;
        stable_sort(vec.begin(), vec.end());

        if(vec[0]*vec[0] + vec[1]*vec[1] == vec[2]*vec[2])
            cout<<"right"<<endl;
        else
            cout<<"wrong"<<endl;
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
input.some((v) => {
  if (v === "0 0 0") return true; // break;

  const nums = v
    .split(" ")
    .map((v) => +v)
    .sort((a, b) => a - b);
  if (nums[0] * nums[0] + nums[1] * nums[1] === nums[2] * nums[2]) {
    console.log("right");
  } else {
    console.log("wrong");
  }
});
```
