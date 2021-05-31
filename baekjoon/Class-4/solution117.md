---
title: "가장 긴 증가하는 부분 수열(11053)"
category: 백준[Class-4]
tags: [C++, JavaScript, 백준]
date: "2021-05-31"
---

## 문제 링크

[가장 긴 증가하는 부분 수열(11053)](https://www.acmicpc.net/problem/11053)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이
void solution(){
    int n;
    cin >> n;

    vector<int> nums;
    nums.push_back(0);
    for(int i=0; i<n; i++){
        int a;
        cin >> a;

        nums.push_back(a);
    }

    vector<int> dp(n+1, 0);     // 부분 수열의 수
    dp[1] = 1;  // 첫 번째
    for(int i=2; i<=n; i++){
        int current = nums[i];
        int max = dp[i];

        for(int j=i-1; j>0; j--){
            if(current > nums[j] && max < dp[j]){
                max = dp[j];
            }
        }

        dp[i] = max+1;
    }

    // 가장 큰 부분 수열의 수 출력
    cout<<*max_element(dp.begin(), dp.end())<<endl;
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
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);

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
const input = fs.readFileSync("dev/stdin").toString().trim().split("\n");

// 문제 풀이
const n = +input[0];
const nums = input[1].split(" ");

const dp = Array(n).fill(0);
dp[0] = 1;
for (let i = 1; i < n; i++) {
  const current = +nums[i];
  let currentCount = dp[i];

  for (let j = 0; j < i; j++) {
    const prev = +nums[j];
    const prevCount = dp[j];

    if (prev < current && currentCount < prevCount) {
      currentCount = prevCount;
    }
  }

  dp[i] = currentCount + 1;
}

// 가장 큰 부분 수열 수 출력
console.log(Math.max(...dp));
```
