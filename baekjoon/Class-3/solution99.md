---
title: "종이의 개수(1780)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-05-20"
---

## 문제 링크

[종이의 개수(1780)](https://www.acmicpc.net/problem/1780)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <map>

using namespace std;

void divide(map<int, int>& log, vector<vector<int> >& board, int size, int row, int col){
    // check
    bool valid = true;
    int value = board[row][col];
    for(int y=row; y<row+size; y++){
        for(int x=col; x<col+size; x++){
            if(value != board[y][x]){
                valid = false;
                break;
            }
        }

        if(!valid) break;
    }

    // divide or logging
    if(!valid){
        // divide
        size /= 3;
        for(int i=0; i<3; i++){
            for(int j=0; j<3; j++){
                divide(log, board, size, row+size*i, col+size*j);
            }
        }
    }
    else{
        // logging
        log[value]++;
    }
}

// 문제 풀이 함수
void solution(){
    int N;
    cin >> N;

    // init
    vector<vector<int> > board;
    for(int i=0; i<N; i++){
        vector<int> vec(N, 0);
        for(int j=0; j<N; j++){
            cin >> vec[j];
        }

        board.push_back(vec);
    }

    // divide
    map<int, int> log;
    log[-1]=0;
    log[0]=0;
    log[1]=0;
    divide(log, board, N, 0, 0);

    // print
    cout<<log[-1]<<"\n"<<log[0]<<"\n"<<log[1]<<"\n";
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
const N = +input[0];

// init
const board = [];
for (let i = 1; i <= N; i++) {
  board.push(input[i].split(" ").map((v) => +v));
}

// recursive function
const log = {
  "-1": 0,
  0: 0,
  1: 0,
};
const divide = (size, row, col) => {
  // check
  let valid = true;
  const value = board[row][col];
  for (let y = row; y < row + size; y++) {
    for (let x = col; x < col + size; x++) {
      if (value !== board[y][x]) {
        valid = false;
        break;
      }
    }
    if (!valid) break;
  }

  if (!valid) {
    // divide-9
    size /= 3;
    for (let i = 0; i < 3; i++) {
      for (let j = 0; j < 3; j++) {
        divide(size, row + i * size, col + j * size);
      }
    }
  } else {
    // logging
    log[value]++;
  }
};

divide(N, 0, 0);

console.log(log[-1]);
console.log(log[0]);
console.log(log[1]);
```
