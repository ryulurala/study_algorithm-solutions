---
title: "최소 힙(1927)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-05-21"
---

## 문제 링크

[최소 힙(1927)](https://www.acmicpc.net/problem/1927)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <queue>

using namespace std;

typedef unsigned int uint;

void solution(){
    int n;
    cin >> n;

    priority_queue<uint, vector<uint>, greater<uint> > pq;
    for(int i=0; i<n; i++){
        int x;
        cin >> x;

        if(x>0){
            pq.push(x);
        }
        else {
            if(!pq.empty()){
                cout<<pq.top()<<"\n";
                pq.pop();
            }
            else {
                cout<<0<<"\n";
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

class MinHeap {
  constructor() {
    this.heap = [];
  }

  isEmpty() {
    return this.heap.length === 0;
  }

  insert(data) {
    this.heap.push(data);

    this.heapifyUp();
  }

  delete() {
    const data = this.heap[0];

    if (this.heap.length > 1) {
      // Swap
      const last = this.heap.length - 1;
      this.heap[0] = this.heap[last];
      this.heap.pop();

      this.heapifyDown();
    } else {
      this.heap.pop();
    }

    return data;
  }

  heapifyUp() {
    let currentIndex = this.heap.length - 1;
    const currentData = this.heap[currentIndex];

    while (currentIndex > 0) {
      const parentIndex = Math.floor((currentIndex - 1) / 2);
      const parentData = this.heap[parentIndex];

      // 부모 값보다 클 경우 종료
      if (currentData >= parentData) break;

      // Swap
      this.heap[currentIndex] = parentData;
      currentIndex = parentIndex;
    }

    // 적당한 위치
    this.heap[currentIndex] = currentData;
  }

  heapifyDown() {
    let currentIndex = 0;
    const currentData = this.heap[currentIndex];

    while (currentIndex < this.heap.length) {
      const leftChildIndex = currentIndex * 2 + 1;
      const rightChildIndex = currentIndex * 2 + 2;

      // 자식 노드가 존재하지 않음
      if (leftChildIndex >= this.heap.length) break;

      const leftChildData = this.heap[leftChildIndex];
      const rightChildData =
        rightChildIndex < this.heap.length ? this.heap[rightChildIndex] : null;

      const smallerIndex =
        rightChildData !== null && rightChildData < leftChildData
          ? rightChildIndex
          : leftChildIndex;
      const smallerData = this.heap[smallerIndex];

      if (currentData <= smallerData) break;

      this.heap[currentIndex] = smallerData;
      currentIndex = smallerIndex;
    }

    // 알맞은 위치
    this.heap[currentIndex] = currentData;
  }
}

// 문제 풀이
const n = +input[0];

const minHeap = new MinHeap();
const log = [];
for (let i = 1; i <= n; i++) {
  const x = +input[i];
  if (x > 0) {
    minHeap.insert(x);
  } else if (minHeap.isEmpty()) {
    log.push(0);
  } else {
    log.push(minHeap.delete());
  }
}

console.log(log.join("\n"));
```
