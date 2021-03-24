---
title: "숫자 카드 2(10816)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-24"
---

## 문제 링크

[숫자 카드 2(10816)](https://www.acmicpc.net/problem/10816)

## C++

```cpp
#include <iostream>
#include <map>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, m, a;
    scanf("%d", &n);

    map<int, int> dictionary;
    for(int i=0; i<n; i++){
        scanf("%d", &a);
        dictionary[a]++;
    }

    scanf("%d", &m);
    for(int i=0; i<m; i++){
        scanf("%d", &a);
        printf("%d ", dictionary[a]);
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
const givenNums = input[1].split(" ");
const m = +input[2];
const checkNums = input[3].split(" ");

const dictionary = {};
givenNums.forEach((v) => {
  if (dictionary[v]) {
    dictionary[v]++;
  } else {
    dictionary[v] = 1;
  }
});

const arr = [];
checkNums.forEach((v) => {
  arr.push(dictionary[v] ? dictionary[v] : 0);
});
console.log(arr.join(" "));
```
