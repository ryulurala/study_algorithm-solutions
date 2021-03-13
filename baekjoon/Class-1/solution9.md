---
title: "OX퀴즈(8958)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-13"
---

## 문제 링크

[OX퀴즈(8958)](https://www.acmicpc.net/problem/8958)

## C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;
    for(int i=0; i<n; i++){
        string str;
        cin >> str;
        int totalScore=0;
        int nextScore=1;
        for(char ch: str){
            if(ch=='O')
                totalScore += nextScore++;
            else if(ch=='X')
                nextScore=1;
        }
        cout<<totalScore<<endl;
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
const input = fs.readFileSync("dev/stdin").toString().split("\n");

// 문제 풀이
const n = input[0];
for (let i = 0; i < n; i++) {
  const str = input[i + 1];
  let totalScore = 0;
  let nextScore = 0;
  for (let j = 0; j < str.length; j++) {
    if (str[j] === "O") totalScore += ++nextScore;
    else if (str[j] === "X") nextScore = 0;
  }
  console.log(totalScore);
}
```
