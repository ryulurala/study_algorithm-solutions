---
title: "균형잡힌 세상(4949)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-22"
---

## 문제 링크

[균형잡힌 세상(4949)](https://www.acmicpc.net/problem/4949)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

// 문제 풀이 함수
void solution(){
    string str;
    while(getline(cin, str)){
        if(str==".") break;

        vector<char> stk;
        for(char ch: str){
            if(ch=='(' || ch=='['){
                stk.push_back(ch);
            }
            else if(ch==')' || ch==']'){
                if(stk.empty()){
                    stk.push_back('x');
                    break;
                }

                if(ch==')' && stk.back()=='('){
                    stk.pop_back();
                }
                else if(ch==']' && stk.back()=='['){
                    stk.pop_back();
                }
                else{
                    break;
                }
            }
        }

        if(stk.empty())
            cout<<"yes\n";
        else
            cout<<"no\n";
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
input
  .filter((v) => v !== ".")
  .forEach((str, i) => {
    str = str.replace(/[^\(\)\[\]]/g, "");

    const stack = [];
    str.split("").some((current) => {
      if (current === "(" || current === "[") {
        stack.push(current);
      } else {
        if (stack.length === 0) {
          stack.push(current);
          return true; // break;
        }

        const top = stack[stack.length - 1];
        if (top === "(" && current === ")") {
          stack.pop();
        } else if (top === "[" && current === "]") {
          stack.pop();
        } else {
          isValid = false;
          return true; // break;
        }
      }
    });

    if (stack.length === 0) console.log("yes");
    else console.log("no");
  });
```
