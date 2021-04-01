---
title: "비밀번호 찾기(17219)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-04-01"
---

## 문제 링크

[비밀번호 찾기(17219)](https://www.acmicpc.net/problem/17219)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <map>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, m;
    cin >> n >> m;

    map<string, string> site_pwd;
    for(int i=0; i<n; i++){
        string site, pwd;
        cin >> site >> pwd;
        site_pwd[site]=pwd;
    }

    for(int i=0; i<m; i++){
        string site;
        cin >> site;
        cout << site_pwd[site] <<"\n";
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

const site_pwd = {};
for (let i = 1; i <= n; i++) {
  input[i] = input[i].split(" ");
  const site = input[i][0];
  const pwd = input[i][1];
  site_pwd[site] = pwd;
}

const log = [];
for (let i = n + 1; i <= n + m; i++) {
  const site = input[i];
  log.push(site_pwd[site]);
}

// print
console.log(log.join("\n"));
```
