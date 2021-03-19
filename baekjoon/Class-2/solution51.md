---
title: "최대공약수와 최소공배수(2609)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-19"
---

## 문제 링크

[최대공약수와 최소공배수(2609)](https://www.acmicpc.net/problem/2609)

## C++

```cpp
#include <iostream>
#include <vector>

using namespace std;

int getGCD(int a, int b){
    if(b==0)
        return a;
    else
        return getGCD(b, a%b);
}

// 문제 풀이 함수
void solution(){
    int a, b;
    cin >> a >> b;

    int gcdAB = getGCD(a, b);
    int lcmAB = a*b/gcdAB;

    cout<<gcdAB<<endl;
    cout<<lcmAB<<endl;
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
const n = +input[0];
const m = +input[1];

const getGCD = (a, b) => {
  if (b === 0) return a;
  else return getGCD(b, a % b);
};

const gcdAB = getGCD(n, m);
const lcmAB = (n * m) / gcdAB;

console.log(gcdAB);
console.log(lcmAB);
```
