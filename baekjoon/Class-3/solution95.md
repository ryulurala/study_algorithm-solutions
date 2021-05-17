---
title: "DFS와 BFS(1260)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-05-17"
---

## 문제 링크

[DFS와 BFS(1260)](https://www.acmicpc.net/problem/1260)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <queue>
#include <stack>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, m, v;
    cin >> n >> m >> v;

    vector<int> graph[n+1];

    for(int i=0; i<m; i++){
        int v1, v2;
        cin >> v1 >> v2;

        graph[v1].push_back(v2);
        graph[v2].push_back(v1);
    }

    // sort
    for(int i=1; i<=n; i++){
        stable_sort(graph[i].begin(), graph[i].end());
    }

    // DFS
    vector<bool> visited(n+1, false);
    stack<int> stk;
    stk.push(v);
    while(!stk.empty()){
        int current = stk.top();
        stk.pop();

        if(!visited[current]){
            visited[current]=true;
            cout<<current<<" ";

            for(int i=graph[current].size()-1; i>=0; i--){
                int next = graph[current][i];
                if(!visited[next]){
                    stk.push(next);
                }
            }
        }
    }

    cout<<"\n";
    // BFS
    for(int i=0; i<visited.size(); i++)
        visited[i] = false;

    queue<int> q;
    q.push(v);
    visited[v]=true;
    cout<<v<<" ";
    while(!q.empty()){
        int current = q.front();
        q.pop();

        for(int i=0; i<graph[current].size(); i++){
            int next = graph[current][i];

            if(!visited[next]){
                visited[next] = true;
                q.push(next);
                cout<<next<<" ";
            }
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

// 문제 풀이
input[0] = input[0].split(" ");
const n = +input[0][0];
const m = +input[0][1];
const v = +input[0][2];

const graph = Array.from({ length: n + 1 }, () => []);
for (let i = 1; i <= m; i++) {
  input[i] = input[i].split(" ");

  const v1 = +input[i][0];
  const v2 = +input[i][1];

  // 연결
  graph[v1].push(v2);
  graph[v2].push(v1);
}

for (const arr of graph) {
  // 오름차순 정렬
  arr.sort((a, b) => a - b);
}

// DFS
const visited = Array.from({ length: n + 1 }, () => false);
const stack = [];
stack.push(v);
const dfsLog = [];
while (stack.length > 0) {
  const current = stack[stack.length - 1];
  stack.pop();

  if (!visited[current]) {
    visited[current] = true;
    dfsLog.push(current);

    // 연결된 정점 순회
    for (let i = graph[current].length - 1; i >= 0; i--) {
      const next = graph[current][i];

      if (!visited[next]) {
        stack.push(next);
      }
    }
  }
}

// BFS
visited.forEach((v, i, arr) => {
  arr[i] = false;
});
const bfsLog = [];
const queue = [];
queue.push(v);
visited[v] = true;
while (queue.length > 0) {
  const current = queue[0];
  bfsLog.push(current);
  queue.shift();

  for (let i = 0; i < graph[current].length; i++) {
    const next = graph[current][i];

    if (!visited[next]) {
      visited[next] = true;
      queue.push(next);
    }
  }
}

// print
console.log(dfsLog.join(" "));
console.log(bfsLog.join(" "));
```
