---
title: "크레인 인형뽑기 게임"
excerpt: "프로그래머스 풀이"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
toc: true
toc_sticky: true
---

## 문제 링크

[크레인 인형뽑기](https://programmers.co.kr/learn/courses/30/lessons/64061)

## C++

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

// board N x N, 5 <= N <= 30
// board 각 칸 0 이상 100 이하, 0은 빈 칸
// moves M, 1 <= M <= 1000

int solution(vector<vector<int>> board, vector<int> moves) {
    int answer = 0;
    int boardSize = board.size();
    int movesLenth = moves.size();
    vector<int> stk;    // 스택 자료구조로 이용

    // todo
    for(int i=0; i<movesLenth; i++){
        int curr = moves[i]-1;
        int item = 0;
        for(int j=0; j<boardSize; j++){
            if(board[j][curr] == 0) continue;
            item = board[j][curr];
            board[j][curr] = 0;
            break;
        }
        if(item != 0){
            // 인형을 집었을 때
            if(!stk.empty() && item == stk.back()){
                // 바구니에 인형이 있고 그 인형과 같다면
                answer += 2;       // 터뜨리기
                stk.pop_back();     // 바구니에서 터뜨린 인형 빼기
            }
            else {
                // 나머지
                stk.push_back(item);
            }
        }
    }

    return answer;
}
```

## JavsScript

```js
function solution(board, moves) {
  var answer = 0;
  let stk = [];

  // todo
  for (let curr of moves) {
    let item = 0;
    for (let i = 0; i < board.length; i++) {
      if (board[i][curr - 1] === 0) continue;
      item = board[i][curr - 1];
      board[i][curr - 1] = 0;
      break;
    }
    if (item != 0) {
      if (stk.length !== 0 && item === stk[stk.length - 1]) {
        answer += 2;
        stk.pop();
      } else {
        stk.push(item);
      }
    }
  }

  return answer;
}
```
