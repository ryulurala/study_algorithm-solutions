---
title: "구간 합 구하기 4(11659)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-04-14"
---

## 문제 링크

[구간 합 구하기 4(11659)](https://www.acmicpc.net/problem/11659)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, m;
    cin >> n >> m;

    int sum=0;
    vector<int> nums(n, 0);
    for(int i=0; i<n; i++){
        int a;
        cin >> a;
        sum += a;
        nums[i] = sum;
    }

    for(int i=0; i<m; i++){
        int a, b;
        cin >> a >> b;
        int firstIdx = min(a-1, b-1);
        int secondIdx = max(a-1, b-1);

        int preSum=firstIdx>0 ? nums[firstIdx-1]:0;
        int sum=nums[secondIdx]-preSum;
        cout<<sum<<"\n";
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
input[0] = input[0].split(" ");
const n = +input[0][0];
const m = +input[0][1];

let sum = 0;
const nums = input[1].split(" ").map((v) => (sum += +v));

const log = [];
for (let i = 2; i < m + 2; i++) {
  input[i] = input[i].split(" ").map((v) => +v);
  const firstIdx = Math.min(input[i][0] - 1, input[i][1] - 1);
  const secondIdx = Math.max(input[i][0] - 1, input[i][1] - 1);

  let preSum = 0;
  if (firstIdx > 0) preSum = nums[firstIdx - 1];

  const sum = nums[secondIdx] - preSum;
  log.push(sum);
}

// print
console.log(log.join("\n"));
```
