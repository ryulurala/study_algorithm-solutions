---
title: "단어 공부(1157)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-13"
---

## 문제 링크

[단어 공부(1157)](https://www.acmicpc.net/problem/1157)

## C++

```cpp
#include <iostream>
#include <map>

using namespace std;

// 문제 풀이 함수
void solution(){
    string str;
    cin >> str;
    for(char& ch: str){
        ch=toupper(ch);
    }
    map<char, int> dict;
    for(char ch: str){
        dict[ch]++;
    }
    int maxCount=0;
    char select;
    for(auto iter: dict){
        char ch=iter.first;
        int count=iter.second;
        if(count>maxCount){
            select=ch;
            maxCount=count;
        } else if(count==maxCount){
            select='?';
        }
    }
    cout<<select<<endl;
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
const input = fs.readFileSync("dev/stdin").toString().trim().split(" ");

// 문제 풀이
const word = input[0].toUpperCase();
const dictionary = {
  A: 0,
  B: 0,
  C: 0,
  D: 0,
  E: 0,
  F: 0,
  G: 0,
  H: 0,
  I: 0,
  J: 0,
  K: 0,
  L: 0,
  M: 0,
  N: 0,
  O: 0,
  P: 0,
  Q: 0,
  R: 0,
  S: 0,
  T: 0,
  U: 0,
  V: 0,
  W: 0,
  X: 0,
  Y: 0,
  Z: 0,
};
word.split("").forEach((v) => {
  dictionary[v]++;
});

let maxCount = 0;
let select;
for (const key in dictionary) {
  const ch = key;
  const count = dictionary[key];
  if (count > maxCount) {
    select = ch;
    maxCount = count;
  } else if (count === maxCount) {
    select = "?";
  }
}
console.log(select);
```
