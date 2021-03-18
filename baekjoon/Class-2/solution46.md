---
title: "설탕 배달(2839)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-18"
---

## 문제 링크

[설탕 배달(2839)](https://www.acmicpc.net/problem/2839)

## C++

```cpp
#include <iostream>
#include <vector>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;

    int total=-1;
    for(int i=0; i<=n/5; i++){
        int rest = n - 5*i;
        if(rest%3==0){
            total= i + rest/3;
        }
    }
    cout<<total<<endl;
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

const maxFive = parseInt(n / 5);
let total = -1;
for (let i = maxFive; i >= 0; i--) {
  const rest = n - i * 5;
  if (rest % 3 === 0) {
    total = i + rest / 3;
    break;
  }
}
console.log(total);
```
