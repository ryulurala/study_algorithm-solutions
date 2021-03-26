---
title: "요세푸스 문제 0(11866)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-26"
---

## 문제 링크

[요세푸스 문제 0(11866)](https://www.acmicpc.net/problem/11866)

## C++

```cpp
#include <iostream>
#include <queue>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, k;
    cin >> n >> k;

    queue<int> q;
    for(int i=1; i<=n; i++){
        q.push(i);
    }

    string log = "<";
    while(!q.empty()){
        for(int i=0; i<k-1; i++){
            int num = q.front();
            q.pop();
            q.push(num);
        }
        int num = q.front();
        q.pop();
        log += to_string(num) + ", ";
    }
    log.pop_back();
    log.pop_back();
    log += ">";
    cout<<log;
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
// split 조절
const input = fs.readFileSync("dev/stdin").toString().trim().split(" ");

// 문제 풀이
const n = +input[0];
const k = +input[1];

const log = [];
const queue = Array.from({ length: n }, (v, i) => i + 1);
while (queue.length > 0) {
  // k-1번 push, pop
  for (let i = 0; i < k - 1; i++) {
    const num = queue.shift();
    queue.push(num);
  }
  const num = queue.shift();
  log.push(num);
}

// print
console.log(`<${log.join(", ")}>`);
```
