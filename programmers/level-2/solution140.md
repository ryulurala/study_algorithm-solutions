---
title: "행렬 테두리 회전하기"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-06-12"
---

## 문제 링크

[행렬 테두리 회전하기](https://programmers.co.kr/learn/courses/30/lessons/77485)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int rotate(vector<vector<int> >& board, int sr, int sc, int er, int ec){
    vector<int> nums;
    nums.push_back(board[sr][sc]);

    int cursor = 0;

    // 우 방향 이동
    for(int x=sc+1; x<=ec; x++){
        int num = board[sr][x];
        nums.push_back(num);

        board[sr][x] = nums[cursor++];
    }

    // 하 방향 이동
    for(int y=sr+1; y<=er; y++){
        int num = board[y][ec];
        nums.push_back(num);

        board[y][ec] = nums[cursor++];
    }

    // 좌 방향 이동
    for(int x=ec-1; x>=sc; x--){
        int num = board[er][x];
        nums.push_back(num);

        board[er][x] = nums[cursor++];
    }

    // 상 방향 이동
    for(int y=er-1; y>=sr; y--){
        int num = board[y][sc];
        nums.push_back(num);

        board[y][sc] = nums[cursor++];
    }

    return *min_element(nums.begin(), nums.end());
}

vector<int> solution(int rows, int columns, vector<vector<int>> queries) {
    vector<int> answer;

    vector<vector<int> > board(rows, vector<int>(columns, 0));

    int count=1;
    for(auto& vec: board){
        for(int& ref: vec){
            ref = count++;
        }
    }

    for(auto vec: queries){
        int startRow = vec[0]-1;
        int startCol = vec[1]-1;
        int endRow = vec[2]-1;
        int endCol = vec[3]-1;

        int minNum = rotate(board, startRow, startCol, endRow, endCol);

        answer.push_back(minNum);
    }


    return answer;
}
```

### JavaScript

```js
function solution(rows, columns, queries) {
  var answer = [];

  // 회전 함수
  const rotate = (board, startY, startX, endY, endX) => {
    const nums = [];
    nums.push(board[startY][startX]);

    // 우 방향 이동
    for (let x = startX + 1; x <= endX; x++) {
      const num = board[startY][x];
      nums.push(num);

      board[startY][x] = nums[nums.length - 2];
    }

    // 하 방향 이동
    for (let y = startY + 1; y <= endY; y++) {
      const num = board[y][endX];
      nums.push(num);

      board[y][endX] = nums[nums.length - 2];
    }

    // 좌 방향 이동
    for (let x = endX - 1; x >= startX; x--) {
      const num = board[endY][x];
      nums.push(num);

      board[endY][x] = nums[nums.length - 2];
    }

    // 상 방향 이동
    for (let y = endY - 1; y >= startY; y--) {
      const num = board[y][startX];
      nums.push(num);

      board[y][startX] = nums[nums.length - 2];
    }

    return Math.min(...nums);
  };

  const board = Array.from({ length: rows }, (v, i) =>
    Array.from({ length: columns }, (vv, ii) => columns * i + ii + 1)
  );

  for (const arr of queries) {
    const [startRow, startCol, endRow, endCol] = arr;

    const minNum = rotate(
      board,
      startRow - 1,
      startCol - 1,
      endRow - 1,
      endCol - 1
    );
    answer.push(minNum);
  }

  return answer;
}
```
