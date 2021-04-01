---
title: "듣보잡(1764)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-04-01"
---

## 문제 링크

[듣보잡(1764)](https://www.acmicpc.net/problem/1764)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <set>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, m;
    cin >> n >> m;

    set<string> names;
    for(int i=0; i<n; i++){
        string str;
        cin >> str;
        names.insert(str);
    }

    vector<string> log;
    for(int j=0; j<m; j++){
        string str;
        cin >> str;
        if(names.count(str)==1)
            log.push_back(str);
    }
    stable_sort(log.begin(), log.end());
    cout<<log.size()<<"\n";
    for(string str: log){
        cout<<str<<"\n";
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
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);

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
const input = fs.readFileSync("dev/stdin").toString().trim().split("\n");

// 문제 풀이
input[0] = input[0].split(" ");
const n = +input[0][0];
const m = +input[0][1];

const map = {};
for (let i = 1; i <= n; i++) {
  const name = input[i];
  if (!map[name]) map[name] = 1;
}

const log = [];
for (let i = n + 1; i <= n + m; i++) {
  const name = input[i];
  if (map[name]) log.push(name);
}
log.sort();
console.log(`${log.length}\n${log.join("\n")}`);
```
