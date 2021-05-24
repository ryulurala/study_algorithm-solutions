---
title: "AC(5430)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-05-24"
---

## 문제 링크

[AC(5430)](https://www.acmicpc.net/problem/5430)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <sstream>
#include <deque>

using namespace std;

void solution(){
    int t;
    cin >> t;

    for(int i=0; i<t; i++){
        deque<int> dq;

        // Init 함수
        string p;
        cin >> p;

        // Init 개수
        int size;
        cin >> size;

        // Init 배열
        string arr;
        cin >> arr;
        arr = arr.substr(1, arr.length()-2);
        stringstream ss(arr);

        string res;
        while(getline(ss, res, ',')){
            int num = stoi(res);
            dq.push_back(num);
        }

        // 함수 처리
        bool reverse=false;
        bool error=false;
        for(char ch: p){
            if(ch=='R'){
                reverse = !reverse;
            }
            else if(ch=='D'){
                if(dq.empty()) error=true;

                if(reverse) dq.pop_back();
                else dq.pop_front();
            }

            if(error) break;
        }

        // print
        if(error){
            cout<<"error\n";
        }
        else if(reverse){
            string log = "[";
            while(!dq.empty()){
                int num = dq.back();
                dq.pop_back();
                log += to_string(num) + ",";
            }

            if(log.back()==',') log.back() = ']';
            else log += "]";

            cout<<log<<"\n";
        }
        else {
            string log = "[";
            while(!dq.empty()){
                int num = dq.front();
                dq.pop_front();
                log += to_string(num) + ",";
            }

            if(log.back()==',') log.back() = ']';
            else log += "]";

            cout<<log<<"\n";
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

// 문제 풀이
const t = +input[0];

let line = 1;
for (let i = 0; i < t; i++) {
  // Init
  const func = input[line++].split("");
  const size = +input[line++];
  const arr = JSON.parse(input[line++]);

  // 함수 처리
  let error = false;
  let reversed = false;
  for (const op of func) {
    if (op === "R") {
      reversed = !reversed;
    } else if (op === "D") {
      if (arr.length > 0) {
        if (reversed) arr.pop();
        else arr.shift();
      } else {
        error = true;
        break;
      }
    }
  }

  // print
  log = error
    ? "error"
    : reversed
    ? JSON.stringify(arr.reverse())
    : JSON.stringify(arr);
  console.log(log);
}
```
