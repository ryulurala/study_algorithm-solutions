---
title: "ACM 호텔(10250)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-16"
---

## 문제 링크

[ACM 호텔(10250)](https://www.acmicpc.net/problem/10250)

## C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    int a, h, w, n;
    cin >> a;
    while(cin >> h >> w >> n){
        int first = n % h;
        first = first==0 ? h : first;

        int last = n / h;
        last = first!=h ? last+1 : last;

        if(last<10)
            cout<<first<<"0"<<last<<endl;
        else
            cout<<first<<last<<endl;
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

for (let i = 1; i <= n; i++) {
  const hwn = input[i].split(" ");
  const h = +hwn[0];
  const w = +hwn[1];
  const n = +hwn[2];

  let first = n % h;
  first = first === 0 ? h : first;

  let last = Math.ceil(n / h);
  last = last < 10 ? "0" + last : last;

  console.log(`${first}${last}`);
}
```
