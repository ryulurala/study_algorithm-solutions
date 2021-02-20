---
title: "경주로 건설"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-20"
---

## 문제 링크

[경주로 건설](https://programmers.co.kr/learn/courses/30/lessons/67259)

### C++

```cpp
#include <string>
#include <vector>
#include <queue>
#include <iostream>

using namespace std;

// 우(0), 하(1), 좌(2), 상(3)
int LUT_ROW[]={0, 1, 0, -1};
int LUT_COL[]={1, 0, -1, 0};

typedef struct Car{
    int row, col, dir, cost;
    Car(int _row, int _col, int _dir, int _cost){
        row=_row;
        col=_col;
        dir=_dir;
        cost=_cost;
    }
}Car;

bool check_visited(vector<vector<vector<int> > >& visited, Car& car){
    int cost=visited[car.row][car.col][car.dir];
    if(cost==0) return false;
    else if(car.cost<cost) return false;    // 적은 비용일 때만
    else return true;   // 이미 방문
}

bool check_arrived(int n, Car& car){
    if(car.row==n-1&&car.col==n-1) return true; // 도착
    else return false;
}

bool check_valid(vector<vector<int> >& board, Car& car){
    int row=car.row;
    int col=car.col;
    if(row<0||col<0) return false;  // 범위 초과
    else if(row>=board.size()||col>=board.size()) return false; // 범위 초과
    else if(board[row][col]==1) return false;   // 벽
    else return true;
}

int solution(vector<vector<int>> board) {
    int answer = 99999999;

    int n=board.size();
    vector<vector<vector<int> > > visited(n, vector<vector<int> >(n, vector<int>(4, 0)));

    queue<Car> q;
    q.push(Car(0, 0, 0, 0));
    q.push(Car(0, 0, 1, 0));

    while(!q.empty()){
        Car& car=q.front();
        q.pop();

        int row=car.row;  // 행
        int col=car.col;  // 열
        int dir=car.dir;    // 방향
        int cost=car.cost;  // 비용

        // 벽 or 보드 안쪽이 아닌 지(유효한 지)
        if(!check_valid(board, car)) continue;

        // 방문했는지
        if(check_visited(visited, car)) continue;
        visited[row][col][dir]=cost;  // 방문체크

        // 도착했는지
        if(check_arrived(n, car)) continue;

        // 직선
        int dRow=row+LUT_ROW[dir];
        int dCol=col+LUT_COL[dir];
        q.push(Car(dRow, dCol, dir, cost+100));

        // 코너
        q.push(Car(row, col, (dir+1)%4, cost+500));
        q.push(Car(row, col, (dir+3)%4, cost+500));
    }

    for(int i=0; i<4; i++){
        int cost=visited[n-1][n-1][i];
        if(cost!=0) answer=min(answer, cost);
    }

    return answer;
}
```

### JavaScript

```js
function solution(board) {
  var answer = 99999999;

  // 우(0), 하(1), 좌(2), 상(3)
  const dirRow = [0, 1, 0, -1];
  const dirCol = [1, 0, -1, 0];

  class Car {
    constructor(row, col, dir, cost) {
      this.row = row;
      this.col = col;
      this.dir = dir;
      this.cost = cost;
    }
  }

  const check_visited = (visited, car) => {
    const cost = visited[car.row][car.col][car.dir];
    if (cost === 0) return false;
    // 방문 X
    else if (cost > car.cost) return false;
    // 비용 적은걸로
    else return true;
  };

  const check_valid = (car) => {
    if (car.row < 0 || car.col < 0) return false;
    // 범위 초과
    else if (car.row >= board.length || car.col >= board.length) return false;
    // 범위
    else if (board[car.row][car.col] === 1) return false;
    // 벽
    else return true;
  };

  const check_arrived = (car) => {
    if (car.row !== board.length - 1) return false;
    else if (car.col !== board.length - 1) return false;
    else return true;
  };

  const visited = Array.from({ length: board.length }, () =>
    Array.from({ length: board.length }, () =>
      Array.from({ length: 4 }, () => 0)
    )
  );

  const q = [];
  q.push(new Car(0, 0, 0, 0));
  q.push(new Car(0, 0, 1, 0));

  // BFS
  while (q.length > 0) {
    const car = q[0];
    q.shift();

    const row = car.row;
    const col = car.col;
    const dir = car.dir;
    const cost = car.cost;

    // 유효한지
    if (!check_valid(car)) continue;

    // 방문했는지
    if (check_visited(visited, car)) continue;
    visited[row][col][dir] = cost;

    // 도착했는지
    if (check_arrived(car)) continue;

    // 직선
    const dRow = car.row + dirRow[car.dir];
    const dCol = car.col + dirCol[car.dir];
    q.push(new Car(dRow, dCol, dir, cost + 100));

    // 코너
    const dir1 = (dir + 1) % 4;
    const dir2 = (dir + 3) % 4;
    q.push(new Car(row, col, dir1, cost + 500));
    q.push(new Car(row, col, dir2, cost + 500));
  }
  for (let i = 0; i < 4; i++) {
    const cost = visited[board.length - 1][board.length - 1][i];
    if (cost !== 0) answer = Math.min(answer, cost); // 방문한 것중에
  }

  return answer;
}
```
