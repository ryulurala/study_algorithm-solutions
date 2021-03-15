---
title: "시험 성적(9498)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-15"
---

## 문제 링크

[시험 성적(9498)](https://www.acmicpc.net/problem/9498)

## C++

```cpp
#include <iostream>

using namespace std;

// 문제 풀이 함수
void solution(){
    int a;
    cin >> a;
    if(a >= 90)
        cout<<"A"<<endl;
    else if(a >= 80)
        cout<<"B"<<endl;
    else if(a >= 70)
        cout<<"C"<<endl;
    else if(a >= 60)
        cout<<"D"<<endl;
    else
        cout<<"F"<<endl;
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
if (n >= 90) {
  console.log("A");
} else if (n >= 80) {
  console.log("B");
} else if (n >= 70) {
  console.log("C");
} else if (n >= 60) {
  console.log("D");
} else {
  console.log("F");
}
```
