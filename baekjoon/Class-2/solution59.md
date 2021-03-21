---
title: "소수 찾기(1978)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-21"
---

## 문제 링크

[소수 찾기(1978)](https://www.acmicpc.net/problem/1978)

## C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <cmath>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, a;
    cin >> n;

    vector<int> nums;
    while(cin >> a){
        nums.push_back(a);
    }

    // for. 최대 길이
    int maxNum = *max_element(nums.begin(), nums.end());

    // 소수 판별 Look up table, 일단 모두 소수
    vector<bool> LUT(maxNum+1, true);
    LUT[0] = false; // 0은 소수 [X]
    LUT[1] = false; // 1은 소수 [X]

    for(int i=2; i<=sqrt(maxNum); i++){
        if(LUT[i]==false) continue; // 이미 소수가 아님

        for(int j=i+i; j<=maxNum; j+=i){
            // 소수의 배수는 소수가 아님
            LUT[j] = false;
        }
    }

    int count=0;
    for(int e: nums){
        if(LUT[e]==true) count++;
    }

    cout<<count<<"\n";
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
const nums = input[1].split(" ").map((v) => +v);

const maxNum = Math.max(...nums); // for. 최대 Length

// Look up table: 일단 0~1000 모두 소수
const LUT = Array.from({ length: maxNum + 1 }, () => true);
LUT[0] = false; // 0은 소수 [X]
LUT[1] = false; // 1은 소수 [X]

for (let i = 2; i <= Math.sqrt(maxNum); i++) {
  if (!LUT[i]) continue; // 이미 소수가 아니면 Pass!

  for (let j = i + i; j <= maxNum; j += i) {
    // 해당 배수는 모두 소수가 아님
    LUT[j] = false;
  }
}

// 소수인 경우만 count 증가
let count = 0;
nums.forEach((v) => {
  if (LUT[v]) count++;
});

console.log(count);
```
