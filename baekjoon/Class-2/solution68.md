---
title: "덱(10866)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-25"
---

## 문제 링크

[덱(10866)](https://www.acmicpc.net/problem/10866)

## C++

```cpp
#include <iostream>
#include <string>
#include <deque>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;

    string str;
    deque<int> dec;
    while(getline(cin , str)){
        string cmd = str.substr(0, 4);

        if(cmd == "push"){
            cmd = str.substr(5, 4);
            if(cmd == "fron"){
                int num = stoi(str.substr(11));
                dec.push_front(num);
            }
            else if(cmd == "back"){
                int num = stoi(str.substr(10));
                dec.push_back(num);
            }
        }
        else if(cmd == "pop_"){
            if(dec.empty()) cout<<-1<<"\n";
            else {
                cmd = str.substr(4, 4);
                int num;
                if(cmd == "fron"){
                    num = dec.front();
                    dec.pop_front();
                }
                else if(cmd == "back"){
                    num = dec.back();
                    dec.pop_back();
                }
                cout<<num<<"\n";
            }
        }
        else if(cmd == "size"){
            cout<<dec.size()<<"\n";
        }
        else if(cmd == "empt"){
            cout<<dec.empty()<<"\n";
        }
        else if(cmd == "fron"){
            if(dec.empty()) cout<<-1<<"\n";
            else cout<<dec.front()<<"\n";
        }
        else if(cmd == "back"){
            if(dec.empty()) cout<<-1<<"\n";
            else cout<<dec.back()<<"\n";
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

const deque = [];
const log = [];
cmd.forEach((v) => {
  switch (v[0]) {
    case "push_front":
      deque.unshift(+v[1]);
      break;
    case "push_back":
      deque.push(+v[1]);
      break;
    case "pop_front":
      if (deque.length === 0) log.push(-1);
      else {
        log.push(deque[0]);
        deque.shift();
      }
      break;
    case "pop_back":
      if (deque.length === 0) log.push(-1);
      else {
        log.push(deque[deque.length - 1]);
        deque.pop();
      }
      break;
    case "size":
      log.push(deque.length);
      break;
    case "empty":
      if (deque.length > 0) log.push(0);
      else log.push(1);
      break;
    case "front":
      if (deque.length > 0) log.push(deque[0]);
      else log.push(-1);
      break;
    case "back":
      if (deque.length > 0) log.push(deque[deque.length - 1]);
      else log.push(-1);
      break;
  }
});

// print
console.log(log.join("\n"));
```
