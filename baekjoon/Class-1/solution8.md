---
title: "음계(2920)"
category: 백준[Class-1]
tags: [C++, JavaScript, 백준]
date: "2021-03-13"
---

## 문제 링크

[음계(2920)](https://www.acmicpc.net/problem/2920)

## C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    string num="";
    for(int i=0; i<8; i++){
        int n;
        cin >> n;
        num += to_string(n);
    }
    if(num=="12345678"){
        cout<<"ascending"<<endl;
    }
    else if(num=="87654321"){
        cout<<"descending"<<endl;
    }
    else{
        cout<<"mixed"<<endl;
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
const input = fs.readFileSync("dev/stdin").toString().split(" ");

// 문제 풀이
const order = parseInt(input.join(""));
if (order === 12345678) {
  console.log("ascending");
} else if (order === 87654321) {
  console.log("descending");
} else {
  console.log("mixed");
}
```
