---
title: "Hashing(15829)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-18"
---

## 문제 링크

[Hashing(15829)](https://www.acmicpc.net/problem/15829)

## C++

```cpp
#include <iostream>
#include <vector>

using namespace std;

// 문제 풀이 함수
void solution(){
    int l;
    string str;
    cin >> l >>str;

    long sum=0;
    long mulR=1;
    for(int i=0; i<l; i++){
        sum += ((str[i]-'a'+1)*mulR) % 1234567891;
        mulR *= 31;
        mulR %= 1234567891;
        sum %= 1234567891;
    }
    cout<<sum<<endl;
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
const l = +input[0];
const str = input[1];

let sum = 0;
let mulR = 1;
for (let i = 0; i < l; i++) {
  sum += ((str[i].charCodeAt() - "a".charCodeAt() + 1) * mulR) % 1234567891;
  mulR *= 31;
  mulR %= 1234567891;
  sum %= 1234567891;
}
console.log(sum);
```
