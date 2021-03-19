---
title: "단어 정렬(1181)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-19"
---

## 문제 링크

[단어 정렬(1181)](https://www.acmicpc.net/problem/1181)

## C++

```cpp
#include <iostream>
#include <vector>
#include <set>
#include <algorithm>

using namespace std;

bool cmp(string a, string b){
    if(a.length()==b.length())
        return a < b;   // 사전 순
    else
        return a.length() < b.length(); // 길이 적은 것부터
}

// 문제 풀이 함수
void solution(){
    int n;
    cin >> n;
    string str;
    set<string> _set;
    while(cin >> str){
        _set.insert(str);  // 중복 제거
    }

    vector<string> words(_set.begin(), _set.end());

    // 정렬
    stable_sort(words.begin(), words.end(), cmp);

    for(string s: words){
        cout<<s<<endl;
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
const _set = new Set();
for (let i = 1; i <= n; i++) {
  _set.add(input[i]); // 중복 제거
}
const words = [..._set];

// 정렬
words.sort((a, b) => {
  if (a.length === b.length) return a > b ? 1 : -1;
  else return a.length > b.length ? 1 : -1;
});

words.forEach((v) => {
  console.log(v);
});
```
