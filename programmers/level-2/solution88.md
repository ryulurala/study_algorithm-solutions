---
title: "프렌즈4블록"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-01"
---

## 문제 링크

[프렌즈4블록](https://programmers.co.kr/learn/courses/30/lessons/17679)

### C++

```cpp
#include <string>
#include <vector>
#include <map>

using namespace std;

bool check(vector<string>& board, int x, int y){
    char ch=board[x][y];
    if(ch=='0') return false;
    else if(ch!=board[x][y+1]) return false;
    else if(ch!=board[x+1][y]) return false;
    else if(ch!=board[x+1][y+1]) return false;
    else return true;
}

void erase(vector<string>& board, int x, int y){
    board[x][y]='0';
    board[x][y+1]='0';
    board[x+1][y]='0';
    board[x+1][y+1]='0';
}

void replace(vector<string>& board, int x, int y){
    for(int i=x-1; i>=0; i--){
        if(board[i][y]!='0'){
            board[x][y]=board[i][y];
            board[i][y]='0';
            break;
        }
    }
}

int solution(int m, int n, vector<string> board) {
    int answer = 0;

    while(true){
        // check
        vector<pair<int, int>> pos;
        for(int i=0; i<m-1; i++){
            for(int j=0; j<n-1; j++){
                if(check(board, i, j)){
                    pos.push_back(make_pair(i, j));
                }
            }
        }

        if(pos.empty()) break;

        // erase
        for(auto iter: pos){
            erase(board, iter.first, iter.second);
        }

        // replace
        for(int i=m-1; i>=0; i--){
            for(int j=n-1; j>=0; j--){
                if(board[i][j]=='0'){
                    replace(board, i, j);
                }
            }
        }
    }

    // 지워진 갯수
    for(string str: board){
        for(char ch: str){
            if(ch=='0') answer++;
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(m, n, board) {
  var answer = 0;

  const check = (x, y) => {
    const ch = board[x][y];
    if (ch == "0") return false;
    else if (ch != board[x][y + 1]) return false;
    else if (ch != board[x + 1][y]) return false;
    else if (ch != board[x + 1][y + 1]) return false;
    else return true;
  };

  const erase = (x, y) => {
    board[x][y] = "0";
    board[x][y + 1] = "0";
    board[x + 1][y] = "0";
    board[x + 1][y + 1] = "0";
  };

  const down = (x, y) => {
    for (let i = x - 1; i >= 0; i--) {
      if (board[i][y] != "0") {
        board[x][y] = board[i][y];
        board[i][y] = "0";
        break;
      }
    }
  };

  // Read Only X
  board = board.map((val) => val.split(""));

  while (true) {
    // check
    const pos = [];
    for (let i = 0; i < m - 1; i++) {
      for (let j = 0; j < n - 1; j++) {
        if (check(i, j)) {
          pos.push([i, j]);
        }
      }
    }

    if (pos.length === 0) break;

    // erase
    pos.forEach((xy) => {
      erase(xy[0], xy[1]);
    });

    // down
    for (let i = m - 1; i >= 0; i--) {
      for (let j = n - 1; j >= 0; j--) {
        if (board[i][j] === "0") {
          down(i, j);
        }
      }
    }
  }

  // 지워진 갯수
  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (board[i][j] === "0") answer++;
    }
  }

  return answer;
}
```
