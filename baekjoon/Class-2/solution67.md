---
title: "큐(10845)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-25"
---

## 문제 링크

[큐(10845)](https://www.acmicpc.net/problem/10845)

## C++

```cpp
#include <iostream>
#include <string>
#include <queue>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;

    string str;
    queue<int> q;
    while(getline(cin , str)){
        string sub = str.substr(0, 3);
        if(sub == "pus"){
            int num = stoi(str.substr(5));
            q.push(num);
        }
        else if(sub == "pop"){
            if(q.empty()) cout<<-1<<"\n";
            else{
                cout<<q.front()<<"\n";
                q.pop();
            }
        }
        else if(sub == "siz"){
            cout<<q.size()<<"\n";
        }
        else if(sub == "emp"){
            if(q.empty()) cout<<1<<"\n";
            else cout<<0<<"\n";
        }
        else if(sub == "fro"){
            if(q.empty()) cout<<-1<<"\n";
            else cout<<q.front()<<"\n";
        }
        else if(sub == "bac"){
            if(q.empty()) cout<<-1<<"\n";
            else cout<<q.back()<<"\n";
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
const cmd = input.filter((v, i) => i > 0).map((v) => v.split(" "));

class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class Queue {
  constructor() {
    this.begin = null;
    this.end = null;
    this.length = 0;
  }
  push(data) {
    const node = new Node(data);
    if (this.length > 0) {
      this.end.next = node;
    } else {
      this.begin = node;
    }

    this.end = node;
    this.length++;
  }
  pop() {
    if (this.length === 0) return -1;

    const node = this.begin;
    this.begin = node.next;
    this.length--;

    return node.data;
  }
  size() {
    return this.length;
  }
  empty() {
    return this.length > 0 ? 0 : 1;
  }
  front() {
    if (this.length > 0) return this.begin.data;
    else return -1;
  }
  back() {
    if (this.length > 0) return this.end.data;
    else return -1;
  }
}

const queue = new Queue();
const log = [];
cmd.forEach((v) => {
  switch (v[0]) {
    case "push":
      queue.push(+v[1]);
      break;
    case "pop":
      log.push(queue.pop());
      break;
    case "size":
      log.push(queue.size());
      break;
    case "empty":
      log.push(queue.empty());
      break;
    case "front":
      log.push(queue.front());
      break;
    case "back":
      log.push(queue.back());
      break;
  }
});

// print
console.log(log.join("\n"));
```
