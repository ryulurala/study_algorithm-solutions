---
title: "제로(10773)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-23"
---

## 문제 링크

[제로(10773)](https://www.acmicpc.net/problem/10773)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

// 문제 풀이 함수
void solution(){
    int k, a;
    cin >> k;

    vector<int> stk;
    while(cin >> a){
        if(a==0){
            stk.pop_back();
        }
        else{
            stk.push_back(a);
        }
    }

    int sum=0;
    for(int e: stk){
        sum+=e;
    }
    cout<<sum<<"\n";
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
const k = +input[0];
const stack = [];
for (let i = 1; i <= k; i++) {
  const num = +input[i];
  if (num === 0) {
    stack.pop();
  } else {
    stack.push(num);
  }
}

console.log(stack.reduce((p, v) => p + v, 0));
```
