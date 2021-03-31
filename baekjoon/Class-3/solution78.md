---
title: "나는야 포켓몬 마스터 이다솜(1620)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-03-31"
---

## 문제 링크

[나는야 포켓몬 마스터 이다솜(1620)](https://www.acmicpc.net/problem/1620)

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

    vector<string> poketmons(n+1);
    map<string, int> dogam;
    for(int i=1; i<=n; i++){
        string str;
        cin >> str;
        poketmons[i]=str;
        dogam[str] = i;
    }

    for(int i=0; i<m; i++){
        string str;
        cin >> str;
        if(str[0]>='0' && str[0]<='9'){
            cout<<poketmons[stoi(str)]<<"\n";
        }
        else{
            cout<<dogam[str]<<"\n";
        }
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

const poketmons = Array.from({ length: n + 1 });
const dictionary = {};
for (let i = 1; i <= n; i++) {
  const poketmon = input[i];
  poketmons[i] = poketmon;
  dictionary[poketmon] = i;
}

const log = [];
for (let i = n + 1; i <= n + m; i++) {
  const cmd = input[i];
  if (isNaN(+cmd)) {
    // 문자
    log.push(dictionary[cmd]);
  } else {
    // 숫자
    log.push(poketmons[+cmd]);
  }
}
console.log(log.join("\n"));
```
