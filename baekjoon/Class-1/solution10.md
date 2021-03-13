---
title: "최소, 최대(10818)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-13"
---

## 문제 링크

[최소, 최대(10818)](https://www.acmicpc.net/problem/10818)

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
    vector<int> vec(n);
    for(int i=0; i<n; i++){
        int num;
        cin >> num;
        vec[i]=num;
    }
    stable_sort(vec.begin(), vec.end());
    cout<<vec.front()<<" "<<vec.back()<<endl;
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
const n = input[0];
const nums = input[1]
  .split(" ")
  .map((v) => +v)
  .sort((a, b) => a - b);
console.log(`${nums[0]} ${nums[nums.length - 1]}`);
```
