---
title: "괄호(9012)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-22"
---

## 문제 링크

[괄호(9012)](https://www.acmicpc.net/problem/9012)

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
    while(getline(cin, str)){
        if(str == "") continue;

        vector<char> stk;
        for(char ch: str){
            if(ch=='(') stk.push_back(ch);
            else{
                if(stk.empty()){
                    stk.push_back('x');
                    break;
                }

                if(stk.back()=='('){
                    stk.pop_back();
                }
                else{
                    break;
                }
            }
        }

        if(stk.empty())
            cout<<"YES\n";
        else
            cout<<"NO\n";
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
input
  .filter((v, i) => i > 0)
  .forEach((str) => {
    const stack = [];
    str.split("").some((v) => {
      if (v === "(") {
        stack.push(v);
      } else {
        if (stack.length === 0) {
          stack.push("x");
          return true; // break;
        }

        const top = stack[stack.length - 1];
        if (top === "(") {
          stack.pop();
        } else {
          return true; // break;
        }
      }
    });

    if (stack.length === 0) console.log("YES");
    else console.log("NO");
  });
```
