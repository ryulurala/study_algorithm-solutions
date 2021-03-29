---
title: "마인크래프트(18111)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-30"
---

## 문제 링크

[마인크래프트(18111)](https://www.acmicpc.net/problem/18111)

## C++

```cpp
#include <iostream>
#include <vector>
#include <map>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, m, b;
    cin >> n >> m >> b;

    map<int, int> height_grounds; // 같은 높이의 땅 수
    for(int i=0; i<n; i++){
        for(int j=0; j<m; j++){
            int a;
            cin >> a;
            height_grounds[a]++;
        }
    }

    // Brute-force: 0 ~ 256
    int minSeconds = 64 * 1000000 * 3;
    int maxHeight = 0;
    for(int i=0; i<=256; i++){
        int height = i;

        int pushCnt=0;  // 인벤토리 넣는 갯수
        int popCnt=0;   // 인벤토리에서 꺼낼 갯수
        for(auto p: height_grounds){
            int hgt = p.first;
            int grounds = p.second;

            if(hgt > height){
                pushCnt += (hgt-height) * grounds;
            }
            else if(hgt < height){
                popCnt += (height-hgt) * grounds;
            }
        }

        // 인벤토리 총 갯수(넣을 갯수 포함) < 꺼낼 갯수
        if(b + pushCnt < popCnt) continue;

        int seconds = pushCnt*2 + popCnt;
        if(seconds <= minSeconds){
            minSeconds = seconds;
            maxHeight = height;
        }
    }
    cout<<minSeconds<<" "<<maxHeight;
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
input[0] = input[0].split(" ");
const n = +input[0][0];
const m = +input[0][1];
const b = +input[0][2];
const board = input
  .filter((v, i) => i > 0)
  .map((v) => v.split(" ").map((v) => +v));

// 같은 블록 묶기
const map = {};
board.forEach((v) => {
  v.forEach((vv) => {
    if (map[vv]) {
      map[vv]++;
    } else {
      map[vv] = 1;
    }
  });
});

// brute-force
let maxHeight = 0;
let minSeconds = 64 * 10000000;
for (let i = 0; i <= 256; i++) {
  const height = i;

  let push = 0;
  let pop = 0;
  for (const h in map) {
    const grounds = map[h];
    if (h > height) {
      // 인벤토리에 넣기
      push += (h - height) * grounds;
    } else if (h < height) {
      // 인벤토리에 빼기
      pop += (height - h) * grounds;
    }
  }

  // 인벤토리 총 블록 수가 꺼낼 블록 수보다 작을 경우
  if (b + push < pop) continue;

  const seconds = push * 2 + pop;
  if (seconds <= minSeconds) {
    // 같아도 높이가 높은 것으로 갱신
    minSeconds = seconds;
    maxHeight = height;
  }
}
console.log(`${minSeconds} ${maxHeight}`);
```
