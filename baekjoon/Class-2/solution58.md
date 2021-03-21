---
title: "수 찾기(1920)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-21"
---

## 문제 링크

[수 찾기(1920)](https://www.acmicpc.net/problem/1920)

## C++

```cpp
#include <iostream>
#include <vector>
#include <set>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, m;
    cin >> n;

    set<int> setA;
    for(int i=0; i<n; i++){
        int a;
        cin >> a;
        setA.insert(a);
    }

    cin >> m;
    vector<int> nums(m);
    for(int i=0; i<m; i++){
        int a;
        cin >> a;
        nums[i] = a;
    }

    for(int e: nums){
        if(setA.find(e) != setA.end()){
            // 찾음
            cout<<1<<"\n";
        }
        else{
            // 못찾음
            cout<<0<<"\n";
        }
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
const m = +input[2];

const arrA = input[1].split(" ").map((v) => +v);
const nums = input[3].split(" ").map((v) => +v);

// 정렬
arrA.sort((a, b) => a - b);

// BST
const bstGo = (tgt) => {
  let left = 0;
  let right = arrA.length - 1;

  while (left <= right) {
    const mid = left + right;
    const curr = arrA[mid];
    if (curr < tgt) {
      left = mid + 1;
    } else if (curr > tgt) {
      right = mid - 1;
    } else {
      // 찾음
      return 1;
      break;
    }
  }
  return 0;
};

const print = nums.map((v) => bstGo(v)).join("\n");

// print
console.log(print);
```
