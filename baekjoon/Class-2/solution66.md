---
title: "스택(10828)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-25"
---

## 문제 링크

[스택(10828)](https://www.acmicpc.net/problem/10828)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;

    string str;
    vector<int> stk;
    while(getline(cin , str)){
        string sub = str.substr(0, 3);
        if(sub == "pus"){
            int num = stoi(str.substr(5));
            stk.push_back(num);
        }
        else if(sub == "pop"){
            if(stk.empty()) cout<<-1<<"\n";
            else{
                cout<<stk.back()<<"\n";
                stk.pop_back();
            }
        }
        else if(sub == "siz"){
            cout<<stk.size()<<"\n";
        }
        else if(sub == "emp"){
            if(stk.empty()) cout<<1<<"\n";
            else cout<<0<<"\n";
        }
        else if(sub == "top"){
            if(stk.empty()) cout<<-1<<"\n";
            else cout<<stk.back()<<"\n";
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
const stack = [];
const log = [];
for (let i = 1; i <= n; i++) {
  const cmd = input[i].split(" ");

  switch (cmd[0]) {
    case "push":
      stack.push(+cmd[1]);
      break;
    case "pop":
      if (stack.length > 0) {
        log.push(stack[stack.length - 1]);
        stack.pop();
      } else log.push(-1);
      break;
    case "size":
      log.push(stack.length);
      break;
    case "empty":
      if (stack.length > 0) log.push(0);
      else log.push(1);
      break;
    case "top":
      if (stack.length > 0) log.push(stack[stack.length - 1]);
      else log.push(-1);
      break;
  }
}
console.log(log.join("\n"));
```
