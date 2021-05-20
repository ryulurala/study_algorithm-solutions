---
title: "찾기(1786)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-05-20"
---

## 문제 링크

[찾기(1786)](https://www.acmicpc.net/problem/1786)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

vector<int> makeLPS(string pattern){
    vector<int> table(pattern.length(), 0);

    int left=0;
    int right=1;
    while(right<pattern.length()){
        while(left>0 && pattern[left] != pattern[right]){
            // 패턴이 맞지 않을 경우
            left = table[left-1];
        }

        if(pattern[left] == pattern[right]){
            // 패턴이 맞을 경우
            table[right] = ++left;
        }

        right++;
    }

    return table;
}

vector<int> doKmp(string parent, string pattern){
    vector<int> lps = makeLPS(pattern);
    vector<int> matched;

    int parentIndex=0;
    int patternIndex=0;
    while(parentIndex < parent.length()){
        while(patternIndex>0 && parent[parentIndex] != pattern[patternIndex]){
            patternIndex = lps[patternIndex-1];
        }

        if(parent[parentIndex] == pattern[patternIndex]){
            if(patternIndex == pattern.length()-1){
                // 패턴 문자 모두 매칭
                matched.push_back(parentIndex-pattern.length()+2);

                // prefix 길이만큼 점프
                patternIndex = lps[patternIndex];
            }
            else {
                // 패턴 문자 1개 매칭
                patternIndex++;
            }
        }

        parentIndex++;
    }

    return matched;
}

void solution(){
    string t, p;
    getline(cin, t);
    getline(cin, p);

    vector<int> matched = doKmp(t, p);
    cout<<matched.size()<<"\n";
    for(int index: matched){
        cout<<index<<" ";
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
const input = fs.readFileSync("dev/stdin").toString().split("\n"); // trim() [X]: 공백 포함

// 문제 풀이
const t = input[0];
const p = input[1];

const makeLPS = (pattern) => {
  const table = Array.from({ length: pattern.length }, () => 0);

  let left = 0;
  let right = 1;
  while (right < pattern.length) {
    while (left > 0 && pattern[left] !== pattern[right]) {
      // prefix !== suffix
      left = table[left - 1];
    }

    if (pattern[left] === pattern[right]) {
      // prefix === suffix
      table[right] = ++left;
    }

    right++;
  }

  return table;
};

const kmp = (parent, pattern) => {
  const lps = makeLPS(pattern);
  let matched = [];

  let parentIdx = 0;
  let patternIdx = 0;
  while (parentIdx < parent.length) {
    while (patternIdx > 0 && parent[parentIdx] !== pattern[patternIdx]) {
      patternIdx = lps[patternIdx - 1];
    }

    if (parent[parentIdx] === pattern[patternIdx]) {
      if (patternIdx === pattern.length - 1) {
        // 문자 모두 매칭
        matched.push(parentIdx - pattern.length + 2);

        // prefix 길이만큼 점프
        patternIdx = lps[patternIdx];
      } else {
        patternIdx++;
      }
    }

    parentIdx++;
  }

  return matched;
};

const matched = kmp(t, p);
console.log(matched.length);
console.log(matched.join(" "));
```
