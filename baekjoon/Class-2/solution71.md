---
title: "스택 수열(1874)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-27"
---

## 문제 링크

[스택 수열(1874)](https://www.acmicpc.net/problem/1874)

## C++

```cpp
#include <iostream>
#include <vector>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, a;
    cin >> n;

    vector<int> vec;
    while(cin >> a){
        vec.push_back(a);
    }

    vector<int> stk;
    string log = "";
    int maxNum = 0;
    for(int e: vec){
        if(e > maxNum){
            for(int i=maxNum+1; i<=e; i++){
                stk.push_back(i);
                log += "+\n";
            }
            maxNum = e;
        }
        else if(stk.back() != e){
            log += "NO";
            break;
        }
        stk.pop_back();
        log += "-\n";
    }
    if(log.substr(log.length()-2) == "NO")
        cout<<"NO";
    else
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
const input = fs.readFileSync("dev/stdin").toString().trim().split("\n");

// 문제 풀이
const n = +input[0];
const nums = input.filter((v, i) => i > 0).map((v) => +v);

const log = [];
const stack = [];
let maxNum = 0;
nums.some((v) => {
  if (v > maxNum) {
    for (let i = maxNum + 1; i <= v; i++) {
      stack.push(i);
      log.push("+");
    }
    maxNum = v;
  } else if (v !== stack[stack.length - 1]) {
    log.push("NO");
    return true; // break;
  }
  stack.pop();
  log.push("-");
});

// print
if (log[log.length - 1] === "NO") console.log("NO");
else console.log(log.join("\n"));
```
