---
title: "알파벳 찾기(10809)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-15"
---

## 문제 링크

[알파벳 찾기(10809)](https://www.acmicpc.net/problem/10809)

## C++

```cpp
#include <iostream>
#include <map>

using namespace std;

// 문제 풀이 함수
void solution(){
    string str;
    cin >> str;
    map<char, int> dictionary;
    for(int i=0; i<26; i++){
        dictionary['a'+i] = -1;
    }
    for(int i=0; i<str.length(); i++){
        char ch = str[i];
        if(dictionary[ch]!=-1) continue;
        dictionary[ch]=i;
    }
    for(auto iter: dictionary){
        cout<<iter.second<<" ";
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
const str = input[0];
const dictionary = {
  a: -1,
  b: -1,
  c: -1,
  d: -1,
  e: -1,
  f: -1,
  g: -1,
  h: -1,
  i: -1,
  j: -1,
  k: -1,
  l: -1,
  m: -1,
  n: -1,
  o: -1,
  p: -1,
  q: -1,
  r: -1,
  s: -1,
  t: -1,
  u: -1,
  v: -1,
  w: -1,
  x: -1,
  y: -1,
  z: -1,
};
str.split("").forEach((v, i) => {
  if (dictionary[v] === -1) {
    dictionary[v] = i;
  }
});

let rst = "";
for (const key in dictionary) {
  rst += dictionary[key] + " ";
}
console.log(rst);
```
