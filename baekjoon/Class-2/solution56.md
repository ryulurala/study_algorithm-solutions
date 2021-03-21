---
title: "좌표 정렬하기(11650)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-21"
---

## 문제 링크

[좌표 정렬하기(11650)](https://www.acmicpc.net/problem/11650)

## C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

bool cmp(pair<int, int> a, pair<int, int> b){
    if(a.first == b.first)
        return a.second < b.second;
    else
        return a.first < b.first;
}

// 문제 풀이 함수
void solution(){
    int n, x, y;
    cin >> n;

    vector<pair<int, int> > xys;
    while(cin >> x >> y){
        xys.push_back({x, y});
    }

    // 정렬
    stable_sort(xys.begin(), xys.end(), cmp);

    for(auto p: xys){
        cout<<p.first<<" "<<p.second<<"\n";
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
const xyList = input.filter((v, i) => i > 0).map((v) => v.split(" "));

// 정렬
xyList.sort((a, b) => {
  if (a[0] === b[0]) return a[1] - b[1];
  else return a[0] - b[0];
});

console.log(xyList.map((v) => v.join(" ")).join("\n"));
```
