---
title: "트리의 부모 찾기(11725)"
category: 백준[Class-4]
tags: [C++, JavaScript, 백준]
date: "2021-05-31"
---

## 문제 링크

[트리의 부모 찾기(11725)](https://www.acmicpc.net/problem/11725)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <queue>

using namespace std;

// 문제 풀이
void solution(){
    int n;
    cin >> n;

    vector<int> graph[n+1];
    for(int i=0; i<n; i++){
        int v1, v2;
        cin >> v1 >> v2;

        // 연결
        graph[v1].push_back(v2);
        graph[v2].push_back(v1);
    }

    // BFS
    vector<int> parent(n+1, 0);
    queue<int> q;
    q.push(1);
    parent[1] = 1;
    while(!q.empty()){
        int current = q.front();
        q.pop();

        // 연결된 정점들
        for(int v: graph[current]){
            if(parent[v] == 0){
                parent[v] = current;
                q.push(v);
            }
        }
    }

    for(int i=2; i<=n; i++){
        cout<<parent[i]<<"\n";
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

const graph = Array.from({ length: n + 1 }, () => []);
for (let i = 1; i < input.length; i++) {
  const [v1, v2] = input[i].split(" ");

  // 연결
  graph[+v1].push(+v2);
  graph[+v2].push(+v1);
}

// BFS
const parent = Array(n + 1).fill(0);
const queue = [];
parent[1] = 1;
queue.push(1);

while (queue.length > 0) {
  const current = queue[0];
  queue.shift(); // pop

  for (const next of graph[current]) {
    if (parent[next] === 0) {
      parent[next] = current;
      queue.push(next);
    }
  }
}

// 2번부터
const log = [];
for (let i = 2; i <= n; i++) {
  log.push(parent[i]);
}

// print
console.log(log.join("\n"));
```
