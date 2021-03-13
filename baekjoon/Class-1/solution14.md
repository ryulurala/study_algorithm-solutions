---
title: "A+B - 5(10952)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-13"
---

## 문제 링크

[A+B - 5(10952)](https://www.acmicpc.net/problem/10952)

## C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    int a, b;
    vector<int> vec;
    while(cin >> a >> b){
        vec.push_back(a+b);
    }
    for(int i=0; i<vec.size()-1; i++){
        cout<<vec[i]<<endl;
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
for (let i = 0; i < input.length - 1; i++) {
  const nums = input[i].split(" ").map((v) => +v);
  console.log(nums[0] + nums[1]);
}
```
