---
title: "기둥과 보 설치"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-12"
---

## 문제 링크

[기둥과 보 설치](https://programmers.co.kr/learn/courses/30/lessons/60061)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

bool kidoong(vector<vector<int> >& board, int x, int y){
    // "기둥"이 있을 조건인지
    if(y==0) return true;   // 제일 밑 바닥
    else if(y>0&&
            (board[x][y-1]==0||board[x][y-1]==2)) return true;     // 기둥 위
    else if(board[x][y]==1||board[x][y]==2) return true;  // 보 왼쪽 위
    else if(x>0&&
            (board[x-1][y]==1||board[x-1][y]==2)) return true; // 보 오른쪽 위
    else return false;  // 나머지
}

bool bo(vector<vector<int> >& board, int x, int y){
    // "보"가 있을 조건인지
    if(y>0&&
       (board[x][y-1]==0||board[x][y-1]==2)) return true;    // 기둥 위
    else if(x<board.size()-1&&y>0&&
            (board[x+1][y-1]==0||board[x+1][y-1]==2)) return true;    // 기둥 위
    else if(x>0&&x<board.size()-1&&board[x-1][y]>=1&&board[x+1][y]>=1) return true;    // 양쪽에 보
    else return false;  // 나머지
}

bool isPossible(vector<vector<int> >& board){
    for(int i=0; i<board.size(); i++){
        for(int j=0; j<board[i].size(); j++){
            if(board[i][j]==-1) continue;
            else if(board[i][j]==2&&kidoong(board, i, j)&&bo(board, i, j)) continue;
            else if(board[i][j]==1&&bo(board, i, j)) continue;
            else if(board[i][j]==0&&kidoong(board, i, j)) continue;
            else return false;
        }
    }
    return true;
}

vector<vector<int>> solution(int n, vector<vector<int>> build_frame) {
    vector<vector<int>> answer;

    vector<vector<int> > board(n+1, vector<int>(n+1, -1));  // [0~n][0~n]
    for(auto vec: build_frame){
        // 옆면을 기준
        int x=vec[0];
        int y=vec[1];
        if(vec[3]==1){
            int origin=board[x][y];     // 백업
            if(origin==-1) board[x][y]=vec[2];  // 설치
            else board[x][y]=2;   // 보 or 기둥이 이미 설치돼있음

            if(!isPossible(board)) board[x][y]=origin;  // 취소
        }
        else if(vec[3]==0){
            int origin=board[x][y];  // 백업
            if(vec[2]==0&&origin==2) board[x][y]=1;     // 보 잔존
            else if(vec[2]==1&&origin==2) board[x][y]=0;  // 기둥 잔존
            else board[x][y]=-1;    // 기둥 or 보 삭제

            if(!isPossible(board)) board[x][y]=origin;  // 취소
        }
    }

    for(int x=0; x<=n; x++){
        for(int y=0; y<=n; y++){
            if(board[x][y]==-1) continue;
            else if(board[x][y]==2){
                vector<int> v1;
                v1.push_back(x);
                v1.push_back(y);
                vector<int> v2(v1);
                v1.push_back(0);
                v2.push_back(1);

                answer.push_back(v1);   // 기둥
                answer.push_back(v2);   // 보
            }
            else {
                vector<int> v;
                v.push_back(x);
                v.push_back(y);
                v.push_back(board[x][y]);
                answer.push_back(v);
            }
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(n, build_frame) {
  var answer = [];

  const kidoong = (board, x, y) => {
    // 해당 (x, y)에 "기둥"이 있어도 되는지
    if (y === 0) return true;
    // 바닥
    else if (y > 0 && (board[x][y - 1] === 0 || board[x][y - 1] === 2))
      return true;
    // 기둥 위
    else if (board[x][y] === 1 || board[x][y] === 2) return true;
    // 왼쪽 보 위
    else if (x > 0 && (board[x - 1][y] === 1 || board[x - 1][y] === 2))
      return true;
    // 오른쪽 보 위
    else return false; // 나머지
  };

  const bo = (board, x, y) => {
    // 해당 (x, y)에 "보"가 있어도 되는지
    if (y > 0 && (board[x][y - 1] === 0 || board[x][y - 1] === 2)) return true;
    // 기둥 위
    else if (
      y > 0 &&
      x < n &&
      (board[x + 1][y - 1] === 0 || board[x + 1][y - 1] === 2)
    )
      return true;
    // 기둥 위
    else if (x > 0 && x < n && board[x - 1][y] >= 1 && board[x + 1][y] >= 1)
      return true;
    // 양쪽 끝에 보
    else return false;
  };

  const canDo = (board) => {
    // 가능한지
    for (let i = 0; i <= n; i++) {
      for (let j = 0; j <= n; j++) {
        if (board[i][j] == -1) continue;
        else if (board[i][j] == 0 && kidoong(board, i, j)) continue;
        else if (board[i][j] == 1 && bo(board, i, j)) continue;
        else if (board[i][j] == 2 && kidoong(board, i, j) && bo(board, i, j))
          continue;
        else return false;
      }
    }
    return true;
  };

  const board = Array.from({ length: n + 1 }, () =>
    Array.from({ length: n + 1 }, () => -1)
  );
  build_frame.forEach((arr) => {
    const x = arr[0];
    const y = arr[1];
    const what = arr[2];
    const doing = arr[3];

    if (doing === 1) {
      // 설치
      const origin = board[x][y];
      if (origin === -1) board[x][y] = what;
      else board[x][y] = 2;

      if (!canDo(board)) board[x][y] = origin; // 취소
    } else {
      // 제거
      const origin = board[x][y];
      if (what === 0 && origin === 2) {
        board[x][y] = 1; // 보 잔존
      } else if (what === 1 && origin === 2) {
        board[x][y] = 0; // 기둥 잔존
      } else board[x][y] = -1;

      if (!canDo(board)) board[x][y] = origin;
    }
  });

  for (let i = 0; i <= n; i++) {
    for (let j = 0; j <= n; j++) {
      if (board[i][j] === -1) continue;
      else if (board[i][j] === 2) {
        answer.push([i, j, 0]);
        answer.push([i, j, 1]);
      } else {
        answer.push([i, j, board[i][j]]);
      }
    }
  }

  return answer;
}
```
