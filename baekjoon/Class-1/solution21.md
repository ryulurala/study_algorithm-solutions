---
title: "숫자의 개수(2577)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-14"
---

## 문제 링크

[숫자의 개수(2577)](https://www.acmicpc.net/problem/2577)

## C++

```cpp
#include <iostream>
#include <map>

using namespace std;

// 문제 풀이 함수
void solution(){
    int total=1;
    int num;
    while(cin >> num){
        total *= num;
    }
    string str = to_string(total);
    map<char, int> dictionary;
    for(int i=0; i<=9; i++){
        char ch = i + '0';
        dictionary[ch]=0;
    }
    for(char ch: str){
        dictionary[ch]++;
    }
    for(auto iter: dictionary){
        cout<<iter.second<<endl;
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
const total = input.reduce((p, v) => p * +v, 1);
const nums = {
  0: 0,
  1: 0,
  2: 0,
  3: 0,
  4: 0,
  5: 0,
  6: 0,
  7: 0,
  8: 0,
  9: 0,
};
total
  .toString()
  .split("")
  .forEach((v) => {
    nums["" + v]++;
  });

for (const key in nums) {
  console.log(nums[key]);
}
```
