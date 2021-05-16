---
title: "유기농 배추(1012)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-05-16"
---

## 문제 링크

[유기농 배추(1012)](https://www.acmicpc.net/problem/1012)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

void bfsGo(vector<vector<int> >& board, int y, int x){
    board[y][x]=0;

    if(y-1>=0 && board[y-1][x]==1)
        bfsGo(board, y-1, x);   // 상
    if(y+1<board.size() && board[y+1][x]==1)
        bfsGo(board, y+1, x);   // 하
    if(x-1>=0 && board[y][x-1]==1)
        bfsGo(board, y, x-1);   // 좌
    if(x+1<board[y].size() && board[y][x+1]==1)
        bfsGo(board, y, x+1);   // 우
}

// 문제 풀이 함수
void solution(){
    int t;
    cin >> t;
    for(int i=0; i<t; i++){
        int m, n, k;
        cin >> m >> n >> k;

        // init
        vector<vector<int> > board(n, vector<int>(m, 0));
        for(int j=0; j<k; j++){
            int x, y;
            cin >> x >> y;

            board[y][x]=1;
        }

        // BFS
        int count=0;
        for(int a=0; a<board.size(); a++){
            for(int b=0; b<board[a].size(); b++){
                if(board[a][b]==1){
                    count++;

                    bfsGo(board, a, b);
                }
            }
        }

        cout<<count<<"\n";
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
const t = +input[0];

const bfsGo = (board, y, x) => {
  board[y][x] = 0;

  if (y - 1 >= 0 && board[y - 1][x] === 1) bfsGo(board, y - 1, x);
  if (y + 1 < board.length && board[y + 1][x] === 1) bfsGo(board, y + 1, x);
  if (x - 1 >= 0 && board[y][x - 1] === 1) bfsGo(board, y, x - 1);
  if (x + 1 < board[0].length && board[y][x + 1] === 1) bfsGo(board, y, x + 1);
};

let cursor = 1;
for (let i = 0; i < t; i++) {
  input[cursor] = input[cursor].split(" ");

  const m = +input[cursor][0];
  const n = +input[cursor][1];
  const board = Array.from({ length: n }, () =>
    Array.from({ length: m }, () => 0)
  );

  const k = +input[cursor][2];

  cursor++;

  // init
  for (let j = 0; j < k; j++) {
    input[cursor] = input[cursor].split(" ");

    const x = +input[cursor][0];
    const y = +input[cursor][1];

    board[y][x] = 1;

    cursor++;
  }

  // BFS
  let count = 0;
  board.forEach((v, i) => {
    v.forEach((vv, ii) => {
      if (vv === 1) {
        bfsGo(board, i, ii);
        count++;
      }
    });
  });
  console.log(count);
}
```
