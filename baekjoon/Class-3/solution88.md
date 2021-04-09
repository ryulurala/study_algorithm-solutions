---
title: "패션왕 신해빈(9375)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-04-09"
---

## 문제 링크

[패션왕 신해빈(9375)](https://www.acmicpc.net/problem/9375)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <map>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;

    for(int i=0; i<n; i++){
        int t;
        cin >> t;

        map<string, int> kinds_clothCount;
        for(int j=0; j<t; j++){
            string cloth, kinds;
            cin >> cloth >> kinds;
            kinds_clothCount[kinds]++;
        }

        int cnt=1;
        for(auto p: kinds_clothCount){
            cnt *= p.second+1;
        }

        cout<<cnt-1<<"\n";
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
const n = +input[0];

let cursor = 0;
for (let i = 1; i <= n; i++) {
  const map = {};
  const t = +input[++cursor];
  for (let j = 1; j <= t; j++) {
    input[j + cursor] = input[j + cursor].split(" ");
    const cloth = input[j + cursor][0];
    const kinds = input[j + cursor][1];

    if (map[kinds]) {
      map[kinds].push(cloth);
    } else {
      map[kinds] = [cloth];
    }
  }
  cursor += t;

  let cnt = 1;
  for (const key in map) {
    cnt *= map[key].length + 1;
  }
  console.log(cnt - 1); // 아무것도 안입을 경우 제외
}
```
