---
title: "랜선 자르기(1654)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-26"
---

## 문제 링크

[랜선 자르기(1654)](https://www.acmicpc.net/problem/1654)

## C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    int k, n;
    cin >> k >> n;

    vector<unsigned int> vec(k);
    for(int i=0; i<k; i++){
        unsigned int num;
        cin >> num;
        vec[i] = num;
    }


    // binary search
    unsigned int left=1;
    unsigned int right=*max_element(vec.begin(), vec.end());
    while(left<=right){
        int mid = (left + right)/2; // 중간값

        // 최대 랜선 개수
        int cnt=0;
        for(unsigned int e: vec){
            cnt += e/mid;
        }

        if(cnt >= n){
            left = mid+1;
        }
        else if(cnt < n){
            right = mid-1;
        }
    }
    cout<<right;
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
const k = +input[0].split(" ")[0];
const n = +input[0].split(" ")[1];

const cables = input.filter((v, i) => i > 0).map((v) => +v);

// Binary search, upper-bound
let left = 1;
let right = Math.max(...cables);
while (left <= right) {
  const mid = parseInt((left + right) / 2);

  const cnt = cables.reduce((p, v) => p + parseInt(v / mid), 0);

  if (cnt >= n) {
    left = mid + 1;
  } else {
    right = mid - 1;
  }
}
console.log(right);
```
