---
title: "1로 만들기(1463)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-04-05"
---

## 문제 링크

[1로 만들기(1463)](https://www.acmicpc.net/problem/1463)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <queue>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;

    queue<pair<int, int> > q;
    vector<bool> visited(n+1, false);
    q.push({n, 0});
    while(!q.empty()){
        int num = q.front().first;
        int cost = q.front().second;
        q.pop();

        if(num < 0 || visited[num])
            continue;
        visited[n] = true;

        if(num == 1){
            cout<<cost;
            break;
        }

        if(num%3 == 0)
            q.push({num/3, cost+1});
        if(num%2 == 0)
            q.push({num/2, cost+1});
        q.push({num-1, cost+1});
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

// 문제 풀이
const n = +input[0];

class Node {
  constructor(num, cost) {
    this.num = num;
    this.cost = cost;
  }
}

const queue = [];
const visited = Array.from({ length: n + 1 }, () => false);
queue.push(new Node(n, 0));
while (queue.length > 0) {
  const num = queue[0].num;
  const cost = queue[0].cost;
  queue.shift();

  if (num < 0 || visited[num]) continue;
  visited[num] = true;

  if (num === 1) {
    console.log(cost);
    break;
  }

  if (num % 3 === 0) queue.push(new Node(num / 3, cost + 1));
  if (num % 2 === 0) queue.push(new Node(num / 2, cost + 1));
  queue.push(new Node(num - 1, cost + 1));
}
```
