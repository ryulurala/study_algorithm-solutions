---
title: "수 정렬하기 2(2751)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-19"
---

## 문제 링크

[수 정렬하기 2(2751)](https://www.acmicpc.net/problem/2751)

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

    vector<int> nums(n);
    for(int i=0; i<n; i++){
        int a;
        cin >> a;
        nums[i]=a;
    }

    // 정렬
    stable_sort(nums.begin(), nums.end());

    for(int& e: nums){
        cout<<e<<"\n";
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
const nums = input.filter((v, i) => i > 0).map((v) => +v);

// 정렬
nums.sort((a, b) => a - b);
console.log(nums.join("\n"));
```
