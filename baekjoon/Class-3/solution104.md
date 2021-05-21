---
title: "최대 힙(11279)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-05-21"
---

## 문제 링크

[최대 힙(11279)](https://www.acmicpc.net/problem/11279)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <queue>

using namespace std;

void solution(){
    int n;
    cin >> n;

    priority_queue<int> pq;
    for(int i=0; i<n; i++){
        int x;
        cin >> x;

        if(x == 0){
            if(!pq.empty()){
                cout<<pq.top()<<"\n";
                pq.pop();
            }
            else {
                cout<<0<<"\n";
            }
        }
        else {
            pq.push(x);
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

class MaxHeap {
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
      [this.heap[0], this.heap[last]] = [this.heap[last], this.heap[0]];
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

      // 부모 값이 자식 값보다 클 경우 종료
      if (currentData < parentData) break;

      // 부모 값이 자식 값보다 작을 경우 부모 값을 내림
      this.heap[currentIndex] = parentData;
      currentIndex = parentIndex;
    }

    this.heap[currentIndex] = currentData;
  }

  heapifyDown() {
    let currentIndex = 0;
    const currentData = this.heap[currentIndex];

    while (currentIndex < this.heap.length) {
      const leftChildIndex = currentIndex * 2 + 1;
      const rightChildIndex = currentIndex * 2 + 2;

      // 자식 노드가 없을 경우
      if (leftChildIndex >= this.heap.length) break;

      const leftChildData = this.heap[leftChildIndex];
      const rightChildData =
        rightChildIndex < this.heap.length ? this.heap[rightChildIndex] : null;

      const biggerIndex =
        rightChildData !== null && rightChildData >= leftChildData
          ? rightChildIndex
          : leftChildIndex;
      const biggerData = this.heap[biggerIndex];

      // 가장 큰 자식 노드보다 클 경우 종료
      if (currentData >= biggerData) break;

      this.heap[currentIndex] = biggerData;
      currentIndex = biggerIndex;
    }

    this.heap[currentIndex] = currentData;
  }
}

// 문제 풀이
const n = +input[0];
const maxHeap = new MaxHeap();

const log = [];
for (let i = 1; i <= n; i++) {
  if (+input[i] === 0) {
    if (!maxHeap.isEmpty()) {
      log.push(maxHeap.delete());
    } else {
      log.push(0);
    }
  } else {
    maxHeap.insert(+input[i]);
  }
}

console.log(log.join("\n"));
```
