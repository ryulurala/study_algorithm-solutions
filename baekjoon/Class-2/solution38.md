---
title: "블랙잭(2798)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-17"
---

## 문제 링크

[블랙잭(2798)](https://www.acmicpc.net/problem/2798)

## C++

```cpp
#include <iostream>
#include <vector>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, m, a;
    cin >> n >> m;

    vector<int> cards;
    while(cin >> a){
        cards.push_back(a);
    }

    int maxSum=0;
    for(int i=0; i<n-2; i++){
        int first = cards[i];
        for(int j=i+1; j<n-1; j++){
            int second = cards[j];
            for(int k=j+1; k<n; k++){
                int third = cards[k];
                int sum=first+second+third;

                if(sum <= m)
                    maxSum=max(sum, maxSum);
            }
        }
    }

    cout<<maxSum;
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
const n = +input[0].split(" ")[0];
const m = +input[0].split(" ")[1];

const cards = input[1].split(" ").map((v) => +v);

let maxSum = 0;
for (let i = 0; i < n - 2; i++) {
  const first = cards[i];
  for (let j = i + 1; j < n - 1; j++) {
    const second = cards[j];
    for (let k = j + 1; k < n; k++) {
      const third = cards[k];
      const sum = first + second + third;

      if (sum <= m) maxSum = Math.max(sum, maxSum);
    }
  }
}

console.log(maxSum);
```
