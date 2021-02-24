---
title: "N-Queen"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-24"
---

## 문제 링크

[N-Queen](https://programmers.co.kr/learn/courses/30/lessons/12952)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

void dfsGo(int& answer, vector<vector<bool> >& board, int level){
    if(level==board.size()) answer++;   // 개수 증가
    else{
        // 가로
        for(int i=0; i<board.size(); i++){
            if(board[level][i]==false){
                vector<vector<bool> > clone(board);  // 복제본

                // check true
                clone[level][i]=true;
                int left=i-1;
                int right=i+1;
                for(int j=level+1; j<clone.size(); j++){
                    // 세로
                    clone[j][i]=true;

                    // 대각선
                    if(left>=0) clone[j][left--]=true;
                    if(right<clone.size()) clone[j][right++]=true;
                }

                dfsGo(answer, clone, level+1);
            }
        }
    }
}

int solution(int n) {
    int answer = 0;
    vector<vector<bool> > board(n, vector<bool>(n, false));

    dfsGo(answer, board, 0);

    return answer;
}
```

### JavaScript

```js
function solution(n) {
  var answer = 0;

  const dfsGo = (row, board) => {
    if (row === n) answer++;
    else {
      for (let col = 0; col < n; col++) {
        if (board[row][col] === 0) {
          // deep copy
          const boardEx = board.map((v) => [...v]);

          // check true
          boardEx[row][col] = 1;
          let forward = row + 1;
          let left = col - 1;
          let right = col + 1;
          while (forward < n) {
            // 대각선
            if (left >= 0) boardEx[forward][left--] = 1;
            if (right < n) boardEx[forward][right++] = 1;

            // 세로
            boardEx[forward++][col] = 1;
          }

          // next
          dfsGo(row + 1, boardEx);
        }
      }
    }
  };

  const board = Array.from({ length: n }, () =>
    Array.from({ length: n }, () => 0)
  );
  dfsGo(0, board);

  return answer;
}
```
