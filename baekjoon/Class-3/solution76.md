---
title: "집합(11723)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-03-30"
---

## 문제 링크

[집합(11723)](https://www.acmicpc.net/problem/11723)

## C++

```cpp
#include <iostream>
#include <vector>

using namespace std;

// 문제 풀이 함수
void solution(){
    int m;
    cin >> m;

    string log = "";
    int bitSet=0;
    for(int i=0; i<=m; i++){
        string op;
        int num;

        cin >> op;
        if(op == "add"){
            cin >> num;
            bitSet |= 1<<(num-1);
        }
        else if(op == "remove"){
            cin >> num;
            bitSet &= ~(1<<(num-1));    // '~' 반전
        }
        else if(op == "check"){
            cin >> num;
            if(bitSet&(1<<(num-1)))
                cout<<"1\n";
            else
                cout<<"0\n";
        }
        else if(op == "toggle"){
            cin >> num;
            bitSet ^= 1<<(num-1);   // XOR
        }
        else if(op == "all"){
            bitSet |= (1<<21)-1;
        }
        else if(op == "empty"){
            bitSet = 0;
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
const m = +input[0];

let bits = 0;
for (let i = 1; i <= m; i++) {
  const cmd = input[i].split(" ");
  const op = cmd[0];
  switch (op) {
    case "add":
      bits |= 1 << (+cmd[1] - 1);
      break;
    case "remove":
      bits &= ~(1 << (+cmd[1] - 1));
      break;
    case "check":
      if (bits & (1 << (+cmd[1] - 1))) console.log(1);
      else console.log(0);
      break;
    case "toggle":
      bits ^= 1 << (+cmd[1] - 1);
      break;
    case "all":
      bits |= (1 << 21) - 1;
      break;
    case "empty":
      bits = 0;
      break;
  }
}
```
