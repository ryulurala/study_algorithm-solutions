---
title: "최댓값(2562번)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-12"
---

## 문제 링크

[최댓값(2562번)](https://www.acmicpc.net/problem/2562)

## C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    vector<int> vec(9);
    for(int i=0; i<9; i++){
        cin >> vec[i];
    }

    auto iter = max_element(vec.begin(), vec.end());
    cout<<*iter<<endl;
    cout<<iter-vec.begin()+1<<endl;
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
const nums = input.map((v) => +v);
const maxNum = Math.max(...nums);
console.log(maxNum);
console.log(nums.indexOf(maxNum) + 1);
```
