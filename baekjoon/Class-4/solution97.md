---
title: "최단경로(1753)"
category: 백준[Class-4]
tags: [C++, JavaScript, 백준]
date: "2021-05-19"
---

## 문제 링크

[최단경로(1753)](https://www.acmicpc.net/problem/1753)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <queue>

using namespace std;

// 문제 풀이 함수
void solution(){
    int V, E, K;
    cin >> V >> E >> K;

    // init
    vector<pair<int, int> > graph[V+1];
    for(int i=0; i<E; i++){
        int u, v, w;
        cin >> u >> v >> w;

        graph[u].push_back({v, w});
    }

    // dijkstra
    const int INF = 0x7fffffff;
    vector<int> dist(V+1, INF);
    priority_queue<pair<int, int> > pq;
    pq.push({0, K});
    dist[K]=0;

    while(!pq.empty()){
        // 최소 거리의 정점 pop
        int weight = -pq.top().first;
        int current = pq.top().second;
        pq.pop();

        if(dist[current] < weight) continue;

        for(auto p: graph[current]){
            // 인접한 정점 검사
            int next = p.first;
            int nextWeight = weight + p.second;

            if(nextWeight < dist[next]){
                // 거쳐서 간 거리가 직선 거리보다 적을 경우
                dist[next] = nextWeight;
                pq.push({-nextWeight, next});
            }
        }
    }

    for(int i=1; i<=V; i++){
        if(dist[i] != INF) cout<<dist[i]<<"\n";
        else cout<<"INF"<<"\n";
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

// min-heap
class Priority_Queue {
  constructor() {
    this.heap = [];
  }

  empty() {
    return this.heap.length === 0;
  }

  enqueue(item) {
    // 끝에 push
    this.heap.push(item);

    // 끝 node를 올바른 위치로 올리기
    this.shiftUp();
  }

  dequeue() {
    const rootNode = this.heap[0];

    if (this.heap.length >= 2) {
      this.heap[0] = this.heap.pop();

      // root node를 올바른 위치로 내리기
      this.shiftDown();
    } else if (this.heap.length === 1) {
      this.heap = [];
    } else {
      return [];
    }

    return rootNode;
  }

  shiftUp() {
    // 마지막 자식 노드의 올바른 인덱스
    let index = this.heap.length - 1;
    const lastNode = this.heap[index];

    // root 노드 전까지
    while (index > 0) {
      const parentIndex = Math.floor((index - 1) / 2);

      // lastNode가 올바른 자리 찾을 때까지
      if (lastNode[0] < this.heap[parentIndex][0]) {
        this.heap[index] = this.heap[parentIndex];
        index = parentIndex;
      } else {
        // 찾음
        break;
      }
    }
    this.heap[index] = lastNode;
  }

  shiftDown() {
    // root부터
    let index = 0;
    const count = this.heap.length;
    const rootNode = this.heap[index];

    while (true) {
      const leftChildIndex = index * 2 + 1;
      const rightChildIndex = index * 2 + 2;

      // priority가 더 작은 index
      let smallerIndex;
      if (leftChildIndex >= count) {
        break;
      } else if (rightChildIndex >= count) {
        smallerIndex = leftChildIndex;
      } else {
        smallerIndex =
          this.heap[leftChildIndex][0] < this.heap[rightChildIndex][0]
            ? leftChildIndex
            : rightChildIndex;
      }

      // 자리 찾기
      if (this.heap[smallerIndex][0] < rootNode[0]) {
        this.heap[index] = this.heap[smallerIndex];
        index = smallerIndex;
      } else {
        break;
      }
    }
    this.heap[index] = rootNode;
  }
}

input[0] = input[0].split(" ");
const V = +input[0][0];
const E = +input[0][1];
const K = +input[1];

// init
const graph = Array.from({ length: V + 1 }, () => []);
for (let i = 2; i < input.length; i++) {
  input[i] = input[i].split(" ");
  const u = +input[i][0];
  const v = +input[i][1];
  const w = +input[i][2];

  graph[u].push([v, w]);
}

// dijkstra
const dist = Array.from({ length: V + 1 }, () => Infinity);
const pq = new Priority_Queue();
pq.enqueue([0, K]);
dist[K] = 0;
while (!pq.empty()) {
  const [weight, current] = pq.dequeue();

  if (dist[current] < weight) continue;

  graph[current].forEach((v) => {
    const next = v[0];
    const nextWeight = weight + v[1];

    if (nextWeight < dist[next]) {
      dist[next] = nextWeight;
      pq.enqueue([nextWeight, next]);
    }
  });
}

// print
const log = dist
  .filter((v, i) => i > 0)
  .map((v) => (v === Infinity ? "INF" : v));
console.log(log.join("\n"));
```
