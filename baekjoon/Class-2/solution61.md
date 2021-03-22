---
title: "카드2(2164)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-22"
---

## 문제 링크

[카드2(2164)](https://www.acmicpc.net/problem/2164)

## C++

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;

    queue<int> q;
    for(int i=1; i<=n; i++){
        q.push(i);
    }

    while(q.size()>1){
        // 버리고
        q.pop();

        // 밑으로 옮기고
        int front = q.front();
        q.pop();
        q.push(front);
    }

    cout<<q.front()<<"\n";
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
const input = fs.readFileSync("dev/stdin").toString().trim().split("\n");

// 문제 풀이
const n = +input[0];

// Linked list로 Queue 구현
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
    this.length = 0;
  }

  push(data) {
    const node = new Node(data);
    if (this.length === 0) {
      this.front = node;
    } else {
      this.back.next = node;
    }

    this.back = node;
    this.length++;
  }

  pop() {
    if (this.length === 0) {
      return false;
    }
    const data = this.front.data;
    this.front = this.front.next;
    this.length--;

    return data;
  }
}

// Linked list Queue
const queue = new Queue();
for (let i = 1; i <= n; i++) {
  queue.push(i);
}

while (queue.length > 1) {
  // 버리고
  queue.pop();

  // 옮기고
  const front = queue.pop();
  queue.push(front);
}

console.log(queue.front.data);
```
