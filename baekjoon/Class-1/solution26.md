---
title: "상수(2908)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-15"
---

## 문제 링크

[상수(2908)](https://www.acmicpc.net/problem/2908)

## C++

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    string a, b;
    cin >> a >> b;

    reverse(a.begin(), a.end());
    reverse(b.begin(), b.end());

    if(stoi(a) > stoi(b)){
        cout<<a<<endl;
    }
    else{
        cout<<b<<endl;
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
const input = fs.readFileSync("dev/stdin").toString().trim().split(" ");

// 문제 풀이
const a = input[0].split("").reverse().join("");
const b = input[1].split("").reverse().join("");

if (+a > +b) {
  console.log(a);
} else {
  console.log(b);
}
```
