---
title: "잃어버린 괄호(1541)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-05-19"
---

## 문제 링크

[잃어버린 괄호(1541)](https://www.acmicpc.net/problem/1541)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

// 문제 풀이 함수
void solution(){
    string exp;
    cin >> exp;

    // '+' 처리
    vector<int> nums;
    nums.push_back(stoi(exp));  // 처음 수
    for(int i=0; i<exp.length(); i++){
        if(exp[i]=='+'){
            int num1 = nums.back();
            int num2 = stoi(exp.substr(i+1));

            nums.pop_back();
            nums.push_back(num1 + num2);
        }
        else if(exp[i]=='-'){
            nums.push_back(stoi(exp.substr(i+1)));
        }
    }

    // '-' 처리
    int result = nums[0];
    for(int i=1; i<nums.size(); i++){
        result -= nums[i];
    }

    cout<<result<<"\n";
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
const exp = input[0].split(/([+-])/g).map((v) => (isNaN(+v) ? v : +v));

// '+' 처리
let idx = 0;
while (idx < exp.length) {
  if (exp[idx] === "+") {
    const result = exp[idx - 1] + exp[idx + 1];
    idx--;
    exp.splice(idx, 3, result);
  }
  idx++;
}

// '-' 처리
idx = 0;
while (idx < exp.length) {
  if (exp[idx] === "-") {
    const result = exp[idx - 1] - exp[idx + 1];
    idx--;
    exp.splice(idx, 3, result);
  }
  idx++;
}

console.log(...exp);
```
