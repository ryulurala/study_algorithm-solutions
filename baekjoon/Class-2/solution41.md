---
title: "팰린드롬수(1259)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-18"
---

## 문제 링크

[팰린드롬수(1259)](https://www.acmicpc.net/problem/1259)

## C++

```cpp
#include <iostream>

using namespace std;

// 문제 풀이 함수
void solution(){
    string str;
    while(cin >> str){
        if(str == "0") break;

        bool isYes=true;
        for(int i=0; i<str.length()/2; i++){
            if(str[i]==str[str.length()-1-i]) continue;
            isYes=false;
            break;
        }

        if(isYes)
            cout<<"yes"<<endl;
        else
            cout<<"no"<<endl;
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
for (let i = 0; i < input.length - 1; i++) {
  const str = input[i];

  let isYes = true;
  for (let i = 0; i < parseInt(str.length / 2); i++) {
    if (str[i] === str[str.length - i - 1]) continue;

    isYes = false;
    break;
  }

  if (isYes) console.log("yes");
  else console.log("no");
}
```
