---
title: "연결 요소의 개수(11724)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-05-21"
---

## 문제 링크

[연결 요소의 개수(11724)](https://www.acmicpc.net/problem/11724)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <map>

using namespace std;

int find_root(map<int, int>& parent, int num){
    if(parent[num] == num) return num;
    else return parent[num]=find_root(parent, parent[num]);
}

void doUnion(map<int, int>& parent, int num1, int num2){
    int rootNum1 = find_root(parent, num1);
    int rootNum2 = find_root(parent, num2);

    // 부모가 다를 경우
    if(rootNum1 != rootNum2){
        parent[rootNum2] = rootNum1;
    }
}

void solution(){
    int n, m;
    cin >> n >> m;

    // Init
    map<int, int> parent;
    for(int i=1; i<=n; i++){
        parent[i] = i;
    }

    // Union
    for(int i=0; i<m; i++){
        int u, v;
        cin >> u >> v;

        doUnion(parent, u, v);
    }

    map<int, int> roots;
    for(int i=1; i<=n; i++){
        int root = find_root(parent, i);

        roots[root] = 1;
    }

    cout<<roots.size()<<"\n";
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

const find_root = (map, num) => {
  if (map[num] === num) return num;
  else return (map[num] = find_root(map, map[num]));
};

const union = (map, num1, num2) => {
  const rootNum1 = find_root(map, num1);
  const rootNum2 = find_root(map, num2);

  // root가 다를 경우
  if (rootNum1 !== rootNum2) {
    map[rootNum2] = rootNum1;
  }
};

// 문제 풀이
input[0] = input[0].split(" ");
const n = +input[0][0];
const m = +input[0][1];

// Init
const map = {};
for (let i = 1; i <= n; i++) {
  map[i] = i;
}

// Union
for (let i = 1; i <= m; i++) {
  input[i] = input[i].split(" ");
  const u = +input[i][0];
  const v = +input[i][1];

  union(map, u, v);
}

const roots = {};
for (let i = 1; i <= n; i++) {
  const root = find_root(map, i);
  roots[root] = true;
}

// 키 갯수
console.log(Object.keys(roots).length);
```
