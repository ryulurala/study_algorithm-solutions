---
title: "블록 이동하기"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-22"
---

## 문제 링크

[블록 이동하기](https://programmers.co.kr/learn/courses/30/lessons/60063)

### C++

```cpp
#include <string>
#include <vector>
#include <queue>
#include <iostream>

using namespace std;

// 우(0), 하(1), 좌(2), 상(3)
int dirRow[]={0, 1, 0, -1};
int dirCol[]={1, 0, -1, 0};

struct Robot{
    int row, col, dir, time;
    Robot(int _row, int _col, int _dir, int _time){
        row=_row;
        col=_col;
        dir=_dir;
        time=_time;
    }
};

bool check_visited(vector<vector<vector<int> > >& visited, Robot& robot){
    int r=robot.row;
    int c=robot.col;
    int dir=robot.dir;
    int time=robot.time;

    int rr=r+dirRow[dir];
    int cc=c+dirCol[dir];
    int dirdir=(dir+2)%4;

    if(visited[r][c][dir]==-1 && visited[rr][cc][dirdir]==-1)  // 방문안했을 경우
        return false;
    else if(visited[r][c][dir]>time && visited[rr][cc][dir]>time)  // 최소가 아닐 경우
        return false;
    else
        return true;
}

bool check_arrived(int size, Robot& robot){
    int r=robot.row;
    int c=robot.col;
    int rr=r+dirRow[robot.dir];
    int cc=c+dirCol[robot.dir];

    if(r==size-1&&c==size-1) return true;
    else if(rr==size-1&&c==size-1) return true;
    else return false;
}

bool check_valid(vector<vector<int> >& board, Robot& robot){
    int r=robot.row;
    int c=robot.col;
    int rr=r+dirRow[robot.dir];
    int cc=c+dirCol[robot.dir];

    if(r<0 || r>=board.size() || c<0 || c>=board.size())
        return false;
    else if(rr<0 || rr>=board.size() || cc<0 || cc>=board.size())
        return false;
    else if(board[r][c]==1 || board[rr][cc]==1)
        return false;
    else
        return true;
}

int solution(vector<vector<int>> board) {
    int answer = 99999999;

    // init, no visited == -1
    int n=board.size();
    vector<vector<vector<int> > > visited(n, vector<vector<int> >(n, vector<int>(4, -1)));

    queue<Robot> q;
    q.push(Robot(0, 0, 0, 0));
    while(!q.empty()){
        Robot robot=q.front();
        q.pop();

        // 기준 좌표
        int r=robot.row;
        int c=robot.col;
        int dir=robot.dir;
        int time=robot.time;

        // 나머지 좌표
        int rr=r+dirRow[dir];
        int cc=c+dirCol[dir];

        // 방문했는지
        if(check_visited(visited, robot)) continue;
        visited[r][c][dir]=time;
        visited[rr][cc][(dir+2)%4]=time;

        // 도착했는지
        if(check_arrived(n, robot)) continue;

        // 이동
        for(int i=0; i<4; i++){
            int moveDir=(dir+i)%4;
            int moveR=r+dirRow[moveDir];
            int moveC=c+dirCol[moveDir];

            Robot moveRobot = Robot(moveR, moveC, dir, time+1);

            // 유효한지
            if(!check_valid(board, moveRobot)) continue;

            q.push(moveRobot);
        }

        // 회전
        for(int i=1; i<=3; i+=2){
            int rotateDir=(dir+i)%4;    // 1, 3

            Robot rotateRobot1=Robot(r, c, rotateDir, time+1);
            Robot rotateRobot2=Robot(rr, cc, rotateDir, time+1);

            // 유효한 지
            // 같은 방향 두 벽 모두 열려 있어야 함
            if(!check_valid(board, rotateRobot1)) continue;
            if(!check_valid(board, rotateRobot2)) continue;

            q.push(rotateRobot1);
            q.push(rotateRobot2);
        }
    }

    // 최소값 추출
    for(int i=0; i<4; i++){
        int time=visited[n-1][n-1][i];
        if(time==-1) continue;
        answer=min(answer, time);
    }

    return answer;
}
```

### JavaScript

```js
function solution(board) {
  var answer = 99999999;

  // struct
  class Robot {
    constructor(row, col, dir, time) {
      this.row = row;
      this.col = col;
      this.dir = dir;
      this.time = time;
    }
  }

  // 우(0), 하(1), 좌(2), 상(3)
  const LUT = [
    [0, 1],
    [1, 0],
    [0, -1],
    [-1, 0],
  ];
  const size = board.length;
  const visited = Array.from({ length: size }, () =>
    Array.from({ length: size }, () => Array.from({ length: 4 }, () => -1))
  );

  const check_visited = (robot) => {
    const r = robot.row;
    const c = robot.col;
    const d = robot.dir;
    const t = robot.time;

    const rr = r + LUT[d][0];
    const cc = c + LUT[d][1];
    const dd = (d + 2) % 4;

    if (visited[r][c][d] === -1 && visited[rr][cc][dd] === -1) return false;
    // 방문한 적이 없는 경우
    else if (visited[r][c][d] > t && visited[rr][cc][dd] > t) return false;
    // 비용이 더 적은 경우
    else return true;
  };

  const check_arrived = (robot) => {
    const r = robot.row;
    const c = robot.col;
    const rr = r + LUT[robot.dir][0];
    const cc = c + LUT[robot.dir][1];

    if (r === size - 1 && c === size - 1) return true;
    else if (rr === size - 1 && cc === size - 1) return true;
    else return false;
  };

  const check_valid = (robot) => {
    const r = robot.row;
    const c = robot.col;
    const rr = r + LUT[robot.dir][0];
    const cc = c + LUT[robot.dir][1];

    if (r < 0 || c < 0 || r >= size || c >= size) return false;
    else if (rr < 0 || cc < 0 || rr >= size || cc >= size) return false;
    else if (board[r][c] === 1 || board[rr][cc] === 1) return false;
    else return true;
  };

  const q = [];
  q.push(new Robot(0, 0, 0, 0));

  // BFS
  while (q.length > 0) {
    const robot = q[0]; // front()
    q.shift(); // pop()

    const r = robot.row;
    const c = robot.col;
    const d = robot.dir;
    const t = robot.time;

    // 나머지 좌표
    const rr = r + LUT[d][0];
    const cc = c + LUT[d][1];

    // 방문했는지
    if (check_visited(robot)) continue;
    visited[r][c][d] = t; // 기준 좌표(순방향)
    visited[rr][cc][(d + 2) % 4] = t; // 역방향

    // 도착했는지
    if (check_arrived(robot)) continue;

    // 이동
    for (let i = 0; i < 4; i++) {
      const dir = (d + i) % 4;
      const mvR = r + LUT[dir][0];
      const mvC = c + LUT[dir][1];

      const mvRobot = new Robot(mvR, mvC, d, t + 1); // 방향은 그대로

      // 유효한지
      if (!check_valid(mvRobot)) continue;

      q.push(mvRobot);
    }

    // 회전
    for (let i = 1; i <= 3; i += 2) {
      const dir = (d + i) % 4; // 1, 3

      const rtRobot1 = new Robot(r, c, dir, t + 1);
      const rtRobot2 = new Robot(rr, cc, dir, t + 1);

      // 유효한지
      // 같은 방향의 2개의 벽 모두 열려야 함.
      if (!check_valid(rtRobot1) || !check_valid(rtRobot2)) continue;

      q.push(rtRobot1);
      q.push(rtRobot2);
    }
  }

  // 최소값
  for (let i = 0; i < 4; i++) {
    const time = visited[size - 1][size - 1][i];
    if (time === -1) continue;
    answer = Math.min(answer, time);
  }

  return answer;
}
```
