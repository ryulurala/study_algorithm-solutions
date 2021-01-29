---
title: "가장 큰 정사각형 찾기"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-30"
---

## 문제 링크

[가장 큰 정사각형 찾기](https://programmers.co.kr/learn/courses/30/lessons/12905)

### C++

```cpp
#include <vector>
#include <iostream>

using namespace std;

int solution(vector<vector<int>> board)
{
    int answer = 0;

    int rowSize=board.size();
    int colSize=board[0].size();

    if(rowSize==1 || colSize==1) return 1;  // 에러 처리

    for(int i=1; i<rowSize; i++){
        for(int j=1; j<colSize; j++){
            if(board[i][j]==0) continue;
            int up=board[i-1][j];
            int left=board[i][j-1];
            int upperLeft=board[i-1][j-1];

            board[i][j]=min(upperLeft, min(up, left))+1;
            answer=max(board[i][j], answer);
        }
    }

    return answer*answer;
}
```

### JavaScript

```js
function solution(board) {
  var answer = 0;

  const rowSize = board.length;
  const colSize = board[0].length;

  if (rowSize === 1 || colSize === 1) return 1; // 에러 처리

  for (let i = 1; i < rowSize; i++) {
    for (let j = 1; j < colSize; j++) {
      if (board[i][j] === 1) {
        const up = board[i - 1][j];
        const left = board[i][j - 1];
        const upperLeft = board[i - 1][j - 1];

        board[i][j] = Math.min(up, left, upperLeft) + 1;
        answer = Math.max(answer, board[i][j]);
      }
    }
  }

  return answer * answer;
}
```
