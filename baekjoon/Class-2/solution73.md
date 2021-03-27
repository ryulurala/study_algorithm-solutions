---
title: "나무 자르기(2805)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-27"
---

## 문제 링크

[나무 자르기(2805)](https://www.acmicpc.net/problem/2805)

## C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, m;
    cin >> n >> m;

    vector<int> trees(n);
    for(int i=0; i<n; i++){
        int a;
        cin >> a;
        trees[i] = a;
    }

    int left=1;
    int right=2000000000;
    while(left <= right){
        int mid = (left+right)/2;

        long long len = 0;
        for(int tree: trees){
            if(tree>mid) len += tree-mid;
        }

        if(len >= m){
            left = mid + 1;
        }
        else{
            right = mid - 1;
        }
    }
    cout<<left-1;
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
input[0] = input[0].split(" ");
const n = +input[0][0];
const m = +input[0][1];
const trees = input[1].split(" ").map((v) => +v);

// binary search
let left = 1;
let right = 2000000000;
while (left <= right) {
  const mid = parseInt((left + right) / 2);
  const len = trees.reduce((p, v) => {
    if (v - mid > 0) return p + (v - mid);
    else return p;
  }, 0);

  if (len >= m) {
    left = mid + 1;
  } else {
    right = mid - 1;
  }
}
console.log(left - 1);
```
