---
title: "IOIOI(5525)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-05-20"
---

## 문제 링크

[IOIOI(5525)](https://www.acmicpc.net/problem/5525)

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

int KMP(string parent, string pattern){
    vector<int> lps = makeLPS(pattern);
    int count=0;

    int parentIndex=0;
    int patternIndex=0;
    while(parentIndex < parent.length()){
        while(patternIndex>0 && parent[parentIndex] != pattern[patternIndex]){
            patternIndex = lps[patternIndex-1];
        }

        if(parent[parentIndex] == pattern[patternIndex]){
            if(patternIndex == pattern.length()-1){
                // 패턴 문자 모두 매칭
                count++;

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

    return count;
}

void solution(){
    int n, m;
    string s;
    cin >> n >> m >> s;

    string pattern = "I";
    for(int i=0; i<n; i++){
        pattern += "OI";
    }

    cout<<KMP(s, pattern)<<"\n";
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
const m = +input[1];
const s = input[2];

const p = "IO".repeat(n) + "I";

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
  let count = 0;

  let parentIdx = 0;
  let patternIdx = 0;
  while (parentIdx < parent.length) {
    while (patternIdx > 0 && parent[parentIdx] !== pattern[patternIdx]) {
      patternIdx = lps[patternIdx - 1];
    }

    if (parent[parentIdx] === pattern[patternIdx]) {
      if (patternIdx === pattern.length - 1) {
        // 문자 모두 매칭
        count++;

        // prefix 길이만큼 점프
        patternIdx = lps[patternIdx];
      } else {
        patternIdx++;
      }
    }

    parentIdx++;
  }

  return count;
};

console.log(kmp(s, p));
```
