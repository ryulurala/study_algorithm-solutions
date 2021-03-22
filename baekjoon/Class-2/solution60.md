---
title: "통계학(2108)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-22"
---

## 문제 링크

[통계학(2108)](https://www.acmicpc.net/problem/2108)

## C++

```cpp
#include <iostream>
#include <vector>
#include <cmath>
#include <algorithm>
#include <map>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, a;
    cin >> n;

    vector<int> nums;
    while(cin >> a){
        nums.push_back(a);
    }

    // 산술평균
    int sum=0;
    for(int e: nums){
        sum += e;
    }
    cout<<round((float)sum/n)<<"\n";

    // 중앙값
    stable_sort(nums.begin(), nums.end());
    cout<<nums[n/2]<<"\n";

    // 최빈값
    map<int, int> counts;
    for(int e: nums){
        counts[e]++;
    }

    // 최대 빈도 개수 추출
    int maxCount=0;
    for(auto p: counts){
        int count=p.second;
        maxCount = max(count, maxCount);
    }

    // 최대 빈도 개수의 Array
    vector<int> maxCounts;
    for(auto p: counts){
        int count=p.second;
        if(count==maxCount)
            maxCounts.push_back(p.first);
    }

    // print
    if(maxCounts.size()>1){
        // 2개 이상일 경우에 두 번째로 작은 값
        stable_sort(maxCounts.begin(), maxCounts.end());
        cout<<maxCounts[1]<<"\n";
    }
    else{
        cout<<maxCounts[0]<<"\n";
    }

    // 범위
    cout<<nums.back()-nums.front()<<"\n";
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

// 산술 평균
nums.sort((a, b) => a - b);
const sum = nums.reduce((p, v) => p + v);
console.log((sum / n).toFixed(0));

// 중앙값
console.log(nums[parseInt(n / 2)]);

// 최빈값
const numCounts = {};
nums.forEach((v) => {
  if (numCounts[v]) {
    numCounts[v]++;
  } else {
    numCounts[v] = 1;
  }
});

// 가장 많은 갯수만 따로 array로 저장
const maxCount = Math.max(...Object.values(numCounts));
const maxCountNums = [];
for (const key in numCounts) {
  if (numCounts[key] === maxCount) {
    maxCountNums.push(key);
  }
}

// print
if (maxCountNums.length > 1) {
  maxCountNums.sort((a, b) => a - b);
  console.log(maxCountNums[1]);
} else {
  console.log(maxCountNums[0]);
}

// 범위
console.log(nums[n - 1] - nums[0]);
```
