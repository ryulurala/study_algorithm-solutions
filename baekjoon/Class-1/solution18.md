---
title: "평균(1546)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-14"
---

## 문제 링크

[평균(1546)](https://www.acmicpc.net/problem/1546)

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
    vector<float> vec(n);
    for(int i=0; i<n; i++){
        float num;
        cin >> num;
        vec[i]=num;
    }
    float maxScore = *max_element(vec.begin(), vec.end());
    float sum = 0;
    for(int score: vec){
        sum += score/maxScore*100;
    }
    printf("%f\n", (double)sum/n);
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
const scores = input[1].split(" ").map((v) => +v);

const maxScore = Math.max(...scores);
const sum = scores.reduce((prev, value) => prev + (value / maxScore) * 100, 0);
console.log(sum / n);
```
