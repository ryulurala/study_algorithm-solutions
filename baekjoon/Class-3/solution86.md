---
title: "색종이 만들기(2630)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-04-08"
---

## 문제 링크

[색종이 만들기(2630)](https://www.acmicpc.net/problem/2630)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

int zeroCnt = 0;
int oneCnt = 0;

void cutBoard(vector<vector<int> >& board, int row, int col, int size){
    int zero = 0;
    int one = 0;
    for(int i=row; i<row+size; i++){
        for(int j=col; j<col+size; j++){
            if(board[i][j]==0) zero++;
            else one++;
        }
    }

    if(zero == size*size) zeroCnt++;
    else if(one == size*size) oneCnt++;
    else {
        cutBoard(board, row, col, size/2);
        cutBoard(board, row+size/2, col, size/2);
        cutBoard(board, row, col+size/2, size/2);
        cutBoard(board, row+size/2, col+size/2, size/2);
    }
}

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;

    vector<vector<int> > board(n, vector<int>(n, 0));
    for(int i=0; i<n; i++){
        for(int j=0; j<n; j++){
            int a;
            cin >> a;
            board[i][j] = a;
        }
    }

    cutBoard(board, 0, 0, n);
    cout<<zeroCnt<<"\n"<<oneCnt<<"\n";
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
const board = input
  .filter((v, i) => i > 0)
  .map((v) => v.split(" ").map((v) => +v));

let zeroCnt = 0;
let oneCnt = 0;
const cutBoard = (row, col, size) => {
  let zero = 0;
  let one = 0;
  for (let i = row; i < row + size; i++) {
    for (let j = col; j < col + size; j++) {
      if (board[i][j] === 0) zero++;
      else one++;
    }
  }

  if (zero === size * size) {
    zeroCnt++;
  } else if (one === size * size) {
    oneCnt++;
  } else {
    cutBoard(row, col, size / 2);
    cutBoard(row + size / 2, col, size / 2);
    cutBoard(row, col + size / 2, size / 2);
    cutBoard(row + size / 2, col + size / 2, size / 2);
  }
};
cutBoard(0, 0, n);

// print
console.log(`${zeroCnt}\n${oneCnt}`);
```
