---
title: "토마토(7576)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-05-23"
---

## 문제 링크

[토마토(7576)](https://www.acmicpc.net/problem/7576)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <queue>

using namespace std;

void solution(){
    int m, n;
    cin >> m >> n;

    // Init
    vector<vector<int> > board;
    for(int i=0; i<n; i++){
        vector<int> vec;
        for(int j=0; j<m; j++){
            int num;
            cin >> num;

            vec.push_back(num);
        }

        board.push_back(vec);
    }

    // Push 익은 토마토
    queue<vector<int> > q;
    for(int y=0; y<board.size(); y++){
        for(int x=0; x<board[y].size(); x++){
            if(board[y][x]==1){
                q.push({y, x, 0});
            }
        }
    }

    // BFS
    int log=0;
    while(!q.empty()){
        int row = q.front()[0];
        int col = q.front()[1];
        int time = q.front()[2];
        q.pop();

        log = time;

        if(row-1>=0 && board[row-1][col]==0){
            board[row-1][col]=1;
            q.push({row-1, col, time+1});
        }
        if(row+1<n && board[row+1][col]==0){
            board[row+1][col]=1;
            q.push({row+1, col, time+1});
        }
        if(col-1>=0 && board[row][col-1]==0){
            board[row][col-1]=1;
            q.push({row, col-1, time+1});
        }
        if(col+1<m && board[row][col+1]==0){
            board[row][col+1]=1;
            q.push({row, col+1, time+1});
        }
    }

    // check
    bool check=true;
    for(int y=0; y<board.size(); y++){
        for(int x=0; x<board[y].size(); x++){
            if(board[y][x]==0){
                check=false;
                break;
            }
        }

        if(!check) break;
    }

    // print
    log = check ? log : -1;
    cout<<log<<"\n";
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

class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class Queue {
  constructor() {
    this.front = null;
    this.back = null;
    this.size = 0;
  }

  push(data) {
    const node = new Node(data);

    if (this.size === 0) {
      this.front = node;
    } else {
      this.back.next = node;
    }

    this.back = node;
    this.size++;
  }

  pop() {
    const node = this.front;

    if (this.size === 1) {
      this.front = null;
      this.back = null;
    } else {
      this.front = node.next;
    }

    this.size--;

    return node.data;
  }
}

// 문제 풀이
input[0] = input[0].split(" ");
const [m, n] = [+input[0][0], +input[0][1]];

const board = Array.from({ length: n }, (v, i) =>
  input[i + 1].split(" ").map((v) => +v)
);

const queue = new Queue();

// Init
board.forEach((v, i) => {
  v.forEach((vv, ii) => {
    if (vv === 1) {
      // 익은 토마토 push
      queue.push({ row: i, col: ii, time: 0 });
    }
  });
});

// BFS
let lastTime = 0;
while (queue.size > 0) {
  const data = queue.pop();
  const [row, col, time] = [data.row, data.col, data.time];

  lastTime = time;

  if (row - 1 >= 0 && board[row - 1][col] === 0) {
    board[row - 1][col] = 1;
    queue.push({ row: row - 1, col: col, time: time + 1 });
  }
  if (row + 1 < n && board[row + 1][col] === 0) {
    board[row + 1][col] = 1;
    queue.push({ row: row + 1, col: col, time: time + 1 });
  }
  if (col - 1 >= 0 && board[row][col - 1] === 0) {
    board[row][col - 1] = 1;
    queue.push({ row: row, col: col - 1, time: time + 1 });
  }
  if (col + 1 < m && board[row][col + 1] === 0) {
    board[row][col + 1] = 1;
    queue.push({ row: row, col: col + 1, time: time + 1 });
  }
}

// check
let check = true;
for (let y = 0; y < board.length; y++) {
  for (let x = 0; x < board[y].length; x++) {
    if (board[y][x] === 0) {
      check = false;
    }
  }

  if (!check) break;
}

// print
lastTime = check ? lastTime : -1;
console.log(lastTime);
```
