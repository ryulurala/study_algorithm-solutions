---
title: "숨바꼭질(1697)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-05-23"
---

## 문제 링크

[숨바꼭질(1697)](https://www.acmicpc.net/problem/1697)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <queue>

using namespace std;

void solution(){
    int n, k;
    cin >> n >> k;

    const int limit = 100000;
    vector<bool> visited(limit+1, false);

    queue<pair<int, int> > q;
    q.push({n, 0});
    visited[n]=true;

    while(!q.empty()){
        int current = q.front().first;
        int time = q.front().second;
        q.pop();

        // 도착했는지
        if(current == k) {
            cout<<time<<"\n";
            break;
        }

        // 뒤로 걷기
        if(current-1>=0 && !visited[current-1]){
            visited[current-1]=true;
            q.push({current-1, time+1});
        }
        // 앞으로 걷기
        if(current+1<=limit && !visited[current+1]){
            visited[current+1]=true;
            q.push({current+1, time+1});
        }
        // 순간이동
        if(current*2<=limit && !visited[current*2]){
            visited[current*2]=true;
            q.push({current*2, time+1});
        }
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

  enqueue(data) {
    const node = new Node(data);

    if (this.size === 0) {
      this.front = node;
    } else {
      this.back.next = node;
    }

    this.back = node;
    this.size++;
  }

  dequeue() {
    const node = this.front;

    if (this.size === 1) {
      this.front = null;
    } else {
      this.front = node.next;
    }

    this.size--;

    return node.data;
  }
}

// 문제 풀이
input[0] = input[0].split(" ");
const [n, k] = [+input[0][0], +input[0][1]];

const limit = 100000;
const visited = Array.from({ length: limit + 1 }, () => false);
const queue = new Queue();
queue.enqueue({ current: n, time: 0 });
visited[n] = true;

while (queue.size > 0) {
  const data = queue.dequeue();
  const [current, time] = [data.current, data.time];

  // 도착했는지
  if (current === k) {
    console.log(time);
    break;
  }

  if (current - 1 >= 0 && !visited[current - 1]) {
    // X-1 이동
    visited[current - 1] = true;
    queue.enqueue({ current: current - 1, time: time + 1 });
  }
  if (current + 1 <= limit && !visited[current + 1]) {
    // X+1 이동
    visited[current + 1] = true;
    queue.enqueue({ current: current + 1, time: time + 1 });
  }
  if (current * 2 <= limit && !visited[current * 2]) {
    // 순간 이동
    visited[current * 2] = true;
    queue.enqueue({ current: current * 2, time: time + 1 });
  }
}
```
