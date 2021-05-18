---
title: "도시 분할 계획(1647)"
category: 백준[Class-5]
tags: [C++, JavaScript, 백준]
date: "2021-05-18"
---

## 문제 링크

[도시 분할 계획(1647)](https://www.acmicpc.net/problem/1647)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
#include <map>

using namespace std;

typedef struct Edge{
    int v1, v2, w;
    Edge(int _v1, int _v2, int _w){
        v1 = _v1;
        v2 = _v2;
        w = _w;
    }
}Edge;

bool cmp(Edge a, Edge b){
    return a.w < b.w;
}

int find(map<int, int>& root, int node){
    if(node == root[node])
        return node;
    else
        return root[node] = find(root, root[node]);
}

// 문제 풀이 함수
void solution(){
    int N, M;
    cin >> N >> M;

    // init
    vector<Edge> edges;
    for(int i=0; i<M; i++){
        int A, B, C;
        cin >> A >> B >> C;

        edges.push_back(Edge(A, B, C));
    }

    // 오름차순 정렬
    stable_sort(edges.begin(), edges.end(), cmp);

    // union-find
    map<int, int> root;
    for(int i=1; i<=N; i++){
        root[i]=i;
    }

    int totalWeight = 0;
    int edgeCount = 0;
    for(Edge edge: edges){
        if(edgeCount >= N-2) break;

        int v1Root = find(root, edge.v1);
        int v2Root = find(root, edge.v2);

        if(v1Root != v2Root){
            // V2의 root를 v1의 root로 지정
            root[v2Root] = v1Root;
            totalWeight += edge.w;
            edgeCount++;
        }
    }

    cout<<totalWeight<<"\n";
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
const N = +input[0][0];
const M = +input[0][1];

// init
const edges = [];
for (let i = 1; i <= M; i++) {
  input[i] = input[i].split(" ");
  const A = +input[i][0];
  const B = +input[i][1];
  const C = +input[i][2];

  edges.push({ A, B, C });
}

// 오름차순 정렬
edges.sort((a, b) => a.C - b.C);

// 크루스칼
const find = (rootNums, num) => {
  if (rootNums[num] === num) return num;
  else return (rootNums[num] = find(rootNums, rootNums[num]));
};

const rootNums = {};
for (let i = 1; i <= N; i++) {
  rootNums[i] = i;
}

let totalCost = 0;
let edgeCount = 0;
for (const edge of edges) {
  // 마지막 길은 제거: 두 마을로 분리
  if (edgeCount >= N - 2) break;

  const root1 = find(rootNums, edge.A);
  const root2 = find(rootNums, edge.B);
  const cost = edge.C;

  if (root1 !== root2) {
    rootNums[root1] = root2;
    totalCost += cost;
    edgeCount++;
  }
}

console.log(totalCost);
```
