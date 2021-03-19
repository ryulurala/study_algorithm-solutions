---
title: "체스판 다시 칠하기(1018)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-19"
---

## 문제 링크

[체스판 다시 칠하기(1018)](https://www.acmicpc.net/problem/1018)

## C++

```cpp
#include <iostream>
#include <vector>

using namespace std;

int getDiffCount(vector<string>& board, int startY, int startX){
    int diffCnt=0;
    string startW="WB";
    string startB="BW";

    for(int y=startY; y<startY+8; y++){
        if((y&1)==0){
            // 짝수
            for(int x=startX; x<startX+8; x++){
                if(board[y][x] != startW[x%2])
                    diffCnt++;
            }
        }
        else{
            // 홀수
            for(int x=startX; x<startX+8; x++){
                if(board[y][x] != startB[x%2])
                    diffCnt++;
            }
        }
    }

    return min(diffCnt, 64-diffCnt);
}

// 문제 풀이 함수
void solution(){
    int n, m;
    cin >> n >> m;
    string str;
    vector<string> board;
    while(cin >> str){
        board.push_back(str);
    }

    int minDiffCount=64;
    for(int i=0; i<=n-8; i++){
        for(int j=0; j<=m-8; j++){
            minDiffCount=min(minDiffCount, getDiffCount(board, i, j));
        }
    }
    cout<<minDiffCount;
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
const board = [];
for (let i = 1; i < input.length; i++) {
  board.push(input[i]);
}

// line 종류 2가지
const startWLine = Array.from({ length: m }, (v, i) =>
  (i & 1) === 0 ? "W" : "B"
).join("");
const startBLine = Array.from({ length: m }, (v, i) =>
  (i & 1) === 0 ? "B" : "W"
).join("");

// 8*8에 대해서 틀린 갯수
const getDiffCnt = (startY, startX) => {
  let diffCnt = 0;
  for (let i = startY; i < startY + 8; i++) {
    if ((i & 1) === 0) {
      // 짝수 Line
      for (let j = startX; j < startX + 8; j++) {
        if (board[i][j] !== startWLine[j]) diffCnt++;
      }
    } else {
      // 홀수 Line
      for (let j = startX; j < startX + 8; j++) {
        if (board[i][j] !== startBLine[j]) diffCnt++;
      }
    }
  }

  return Math.min(diffCnt, 64 - diffCnt);
};

// 결과 도출: brute-force
let minDiffCnt = 64;
for (let i = 0; i <= n - 8; i++) {
  for (let j = 0; j <= m - 8; j++) {
    minDiffCnt = Math.min(minDiffCnt, getDiffCnt(i, j));
  }
}

console.log(minDiffCnt);
```
